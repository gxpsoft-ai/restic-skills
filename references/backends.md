# Restic Backend Storage Guide

Restic supports various storage backends for repository storage.

## Local Repository

Simplest backend - stores repository in local directory.

```bash
# Using environment variables
export RESTIC_REPOSITORY=/srv/restic-repo
export RESTIC_PASSWORD=your-password
restic init

# Using command line
restic -r /srv/restic-repo init
```

## SFTP (SSH)

Remote repository over SSH.

```bash
# Basic syntax
restic -r sftp:user@host:/path/to/repo init

# With SSH key
restic -r sftp:user@host:/path/to/repo init

# Using key file
restic -r sftp:user@host:/path/to/repo -o ssh.key=/path/to/key init
```

Environment variables:
- `RESTIC_SSH_KEY` - SSH key path

## REST Server

HTTP REST API backend.

```bash
# Server running locally
restic -r rest:http://localhost:8000/ init

# With authentication
restic -r rest:https://user:pass@backup.example.com/ init

# Using environment
export RESTIC_REPOSITORY=rest:http://localhost:8000/
```

## Amazon S3

AWS S3 storage.

```bash
# Using environment variables
export AWS_ACCESS_KEY_ID=your-access-key
export AWS_SECRET_ACCESS_KEY=your-secret-key
restic -r s3:s3.amazonaws.com/bucket-name init

# Using environment
export RESTIC_REPOSITORY=s3:s3.amazonaws.com/bucket-name

# With custom endpoint
restic -r s3:https://nyc3.digitaloceanspaces.com/my-bucket init
```

Options:
- `--s3.region` - S3 region (default: us-east-1)
- `--s3.endpoint` - Custom endpoint
- `--s3.accelerate` - Use S3 Transfer Acceleration
- `--s3.v4-signature` - Force v4 signatures

Environment variables:
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_DEFAULT_REGION`
- `AWS_SESSION_TOKEN` (for temporary credentials)

## Minio Server

Self-hosted S3-compatible storage.

```bash
# Connect to Minio server
restic -r s3:http://localhost:9000/mybucket init

# With credentials
export MINIO_ACCESS_KEY=minioadmin
export MINIO_SECRET_KEY=minioadmin
restic -r s3:http://localhost:9000/mybucket init
```

## S3-Compatible Storage

Various S3-compatible services.

### Wasabi

```bash
restic -r s3:s3.wasabisys.com/bucket-name init

# With region
restic -r s3:s3.us-west-1.wasabisys.com/bucket-name init
```

### Backblaze B2

```bash
# Using B2 backend
restic -r b2:bucket-name init

# With application key
export B2_ACCOUNT_INFO=accountId:applicationKey
restic -r b2:bucket-name init

# Or use environment
export RESTIC_REPOSITORY=b2:bucket-name
export B2_ACCOUNT_INFO=accountId:applicationKey
```

Environment variables:
- `B2_ACCOUNT_INFO` - Account ID and application key (colon-separated)
- `B2_KEY_ID` - Key ID
- `B2_KEY` - Application key
- `B2_ENDPOINT` - Custom endpoint

### Alibaba Cloud OSS

```bash
# Using Aliyun OSS
restic -r s3:https://oss-cn-hangzhou.aliyuncs.com/bucket-name init

# With environment
export ALIBABA_CLOUD_ACCESS_KEY_ID=your-key-id
export ALIBABA_CLOUD_ACCESS_KEY_SECRET=your-key-secret
restic -r s3:https://oss-cn-hangzhou.aliyuncs.com/bucket-name init
```

Environment variables:
- `ALIBABA_CLOUD_ACCESS_KEY_ID`
- `ALIBABA_CLOUD_ACCESS_KEY_SECRET`

### Google Cloud Storage

```bash
# Using GCS
restic -r gs:bucket-name init

# With project
restic -r gs:bucket-name -o gs.project_id=my-project init
```

Environment variables:
- `GOOGLE_APPLICATION_CREDENTIALS` - Path to credentials JSON

## OpenStack Swift

```bash
# Basic Swift
restic -r swift:container-name:path init

# With authentication
export OS_AUTH_URL=https://auth.example.com/v3
export OS_TENANT_ID=tenant-id
export OS_TENANT_NAME=tenant-name
export OS_USERNAME=username
export OS_PASSWORD=password
restic -r swift:container-name init
```

Environment variables:
- `OS_AUTH_URL`
- `OS_TENANT_ID` or `OS_PROJECT_ID`
- `OS_TENANT_NAME` or `OS_PROJECT_NAME`
- `OS_USERNAME`
- `OS_PASSWORD`
- `OS_REGION_NAME`

## Microsoft Azure Blob Storage

```bash
# Using Azure
restic -r azure:container-name init

# With account name
restic -r azure:container-name -o azure.account_name=myaccount init
```

Environment variables:
- `AZURE_STORAGE_ACCOUNT`
- `AZURE_STORAGE_KEY` or `AZURE_STORAGE_SAS_TOKEN`

## rclone Backend

Access any storage that rclone supports.

```bash
# Using rclone remote
restic -r rclone:remote:path init

# Examples:
# Google Drive
restic -r rclone:gdrive:backups init

# Dropbox
restic -r rclone:dropbox:backups init

# OneDrive
restic -r rclone:onedrive:backups init
```

Configuration (via rclone config):
```bash
rclone config
# Follow prompts to set up remote storage
```

## Password Handling

### Password File
```bash
# Using password file
restic -r /srv/repo --password-file /path/to/password.txt init

# Or environment
export RESTIC_PASSWORD_FILE=/path/to/password.txt
```

### Password Command
```bash
# Using password command
restic -r /srv/repo --password-command "echo mypassword" init

# Or environment
export RESTIC_PASSWORD_COMMAND="security find-internet-password -s restic"
```

### Environment Variable
```bash
# Direct password
export RESTIC_PASSWORD=mysecretpassword
restic -r /srv/repo init
```

### Interactive Password
```bash
# Will prompt for password
restic -r /srv/repo init
```

## Repository File

Store repository location in a file:

```bash
# Create repository file
echo "/srv/repo" > ~/.restic-repo

# Use repository file
restic --repository-file ~/.restic-repo snapshots
# Or
export RESTIC_REPOSITORY_FILE=~/.restic-repo
restic snapshots
```

## Multiple Repositories

Manage multiple repositories:

```bash
# Repository 1
export RESTIC_REPOSITORY=/backup/local
export RESTIC_PASSWORD_FILE=~/.backup-password

# Repository 2 (in script)
RESTIC_REPOSITORY=/backup/remote RESTIC_PASSWORD=pass restic -r sftp:host:/path snapshots
```

## Group-Accessible Repositories

Shared repositories for multiple users:

```bash
# Initialize with group permissions
restic init --repo /shared/repo

# Set permissions
chmod -R g+rwX /shared/repo
chgrp -R backupgroup /shared/repo
```

## Empty Password Repositories

For testing or unencrypted local backups:

```bash
# Initialize with empty password
restic --insecure-no-password init

# Or use option
restic -r /test/repo init --insecure-no-password
```
