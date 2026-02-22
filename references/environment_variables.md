# Restic Environment Variables

## Repository Configuration

### RESTIC_REPOSITORY
Location of the repository. Can be a local path or remote backend URL.

```bash
# Local
export RESTIC_REPOSITORY=/srv/restic-repo

# SFTP
export RESTIC_REPOSITORY=sftp:user@host:/path

# S3
export RESTIC_REPOSITORY=s3:s3.amazonaws.com/bucket

# REST
export RESTIC_REPOSITORY=rest:http://localhost:8000/
```

### RESTIC_REPOSITORY_FILE
Path to a file containing the repository location.

```bash
echo "/srv/repo" > ~/.restic-repo
export RESTIC_REPOSITORY_FILE=~/.restic-repo
```

## Password Configuration

### RESTIC_PASSWORD
The password for the repository.

```bash
export RESTIC_PASSWORD=my-secret-password
```

### RESTIC_PASSWORD_FILE
Path to a file containing the repository password.

```bash
echo "my-secret-password" > ~/.restic-password
export RESTIC_PASSWORD_FILE=~/.restic-password
```

### RESTIC_PASSWORD_COMMAND
Command to execute to obtain the repository password.

```bash
# Using a command
export RESTIC_PASSWORD_COMMAND="echo my-password"

# Using a password manager
export RESTIC_PASSWORD_COMMAND="pass restic/backup"
export RESTIC_PASSWORD_COMMAND="security find-internet-password -s restic"
export RESTIC_PASSWORD_COMMAND="keyring get restic backup"
```

### RESTIC_KEY_HINT
Key ID of key to try first when unlocking repository (speeds up multi-key repos).

```bash
export RESTIC_KEY_HINT=key-12345678
```

## AWS/S3 Configuration

### AWS_ACCESS_KEY_ID
AWS access key for S3 backends.

### AWS_SECRET_ACCESS_KEY
AWS secret key for S3 backends.

### AWS_DEFAULT_REGION
AWS region (default: us-east-1).

### AWS_SESSION_TOKEN
AWS session token for temporary credentials.

```bash
export AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
export AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
export AWS_DEFAULT_REGION=us-west-2
```

## Google Cloud Configuration

### GOOGLE_APPLICATION_CREDENTIALS
Path to JSON credentials file for Google Cloud Storage.

```bash
export GOOGLE_APPLICATION_CREDENTIALS=/path/to/credentials.json
```

### GS_PROJECT_ID
Google Cloud project ID.

```bash
export GS_PROJECT_ID=my-project-id
```

## Azure Configuration

### AZURE_STORAGE_ACCOUNT
Azure storage account name.

### AZURE_STORAGE_KEY
Azure storage account key.

### AZURE_STORAGE_SAS_TOKEN
Azure SAS token (for SAS authentication).

```bash
export AZURE_STORAGE_ACCOUNT=mystorageaccount
export AZURE_STORAGE_KEY=base64-encoded-key
```

## Alibaba Cloud Configuration

### ALIBABA_CLOUD_ACCESS_KEY_ID
Aliyun access key ID.

### ALIBABA_CLOUD_ACCESS_KEY_SECRET
Aliyun access key secret.

```bash
export ALIBABA_CLOUD_ACCESS_KEY_ID=LTAI...
export ALIBABA_CLOUD_ACCESS_KEY_SECRET=secret...
```

## Backblaze B2 Configuration

### B2_ACCOUNT_INFO
Account ID and application key (colon-separated).

```bash
export B2_ACCOUNT_INFO=accountId:applicationKey
```

### B2_KEY_ID
B2 key ID (alternative to B2_ACCOUNT_INFO).

### B2_KEY
B2 application key (alternative to B2_ACCOUNT_INFO).

### B2_ENDPOINT
Custom B2-compatible endpoint.

```bash
export B2_KEY_ID=your-key-id
export B2_KEY=your-app-key
```

## OpenStack Swift Configuration

### OS_AUTH_URL
Authentication URL for OpenStack.

### OS_TENANT_ID or OS_PROJECT_ID
Project/tenant ID.

### OS_TENANT_NAME or OS_PROJECT_NAME
Project/tenant name.

### OS_USERNAME
Username.

### OS_PASSWORD
Password.

### OS_REGION_NAME
Region name.

### OS_DOMAIN_NAME
Domain name.

```bash
export OS_AUTH_URL=https://identity.example.com/v3
export OS_TENANT_ID=tenant-id
export OS_USERNAME=user
export OS_PASSWORD=pass
export OS_REGION_NAME=region1
```

## SSH/SFTP Configuration

### RESTIC_SSH_KEY
Path to SSH key for SFTP backend.

```bash
export RESTIC_SSH_KEY=/path/to/private/key
```

### GIT_SSH_COMMAND
SSH command (used for SFTP).

```bash
export GIT_SSH_COMMAND="ssh -i /path/to/key"
```

## Cache Configuration

### RESTIC_CACHE_DIR
Location of the cache directory.

```bash
# Default locations:
# Linux: ~/.cache/restic
# macOS: ~/Library/Caches/restic
# Windows: %LOCALAPPDATA%\restic

# Custom location
export RESTIC_CACHE_DIR=/tmp/restic-cache
```

### XDG_CACHE_HOME
XDG base directory for caches (default: ~/.cache).

```bash
export XDG_CACHE_HOME=/custom/cache
# Cache will be at: /custom/cache/restic
```

## Performance Tuning

### RESTIC_READ_CONCURRENCY
Number of files to read concurrently during backup (default: 2).

```bash
export RESTIC_READ_CONCURRENCY=8
```

### RESTIC_PACK_SIZE
Target pack size in MiB (default: determined by repository format).

```bash
export RESTIC_PACK_SIZE=64
```

### RESTIC_COMPRESSION
Compression mode for repository format v2 (default: auto).

```bash
# Options: auto, off, max
export RESTIC_COMPRESSION=max
```

### RESTIC_PROGRESS_FPS
Progress reporting frequency in frames per second.

```bash
# Update once per second (default)
export RESTIC_PROGRESS_FPS=1

# Update once per minute
export RESTIC_PROGRESS_FPS=0.016666

# Disable progress
export RESTIC_PROGRESS_FPS=0
```

## Network Configuration

### RESTIC_LIMIT_DOWNLOAD
Maximum download speed in KiB/s.

```bash
export RESTIC_LIMIT_DOWNLOAD=10240  # 10 MiB/s
```

### RESTIC_LIMIT_UPLOAD
Maximum upload speed in KiB/s.

```bash
export RESTIC_LIMIT_UPLOAD=5120  # 5 MiB/s
```

### http_proxy / https_proxy / HTTP_PROXY / HTTPS_PROXY
Proxy settings for HTTP/HTTPS backends.

```bash
export http_proxy=http://proxy.example.com:8080
export https_proxy=http://proxy.example.com:8080
```

### no_proxy / NO_PROXY
Hosts to bypass proxy.

```bash
export no_proxy=localhost,127.0.0.1,.local
```

## Snapshot Configuration

### RESTIC_HOST
Hostname for snapshot (default: current hostname).

```bash
export RESTIC_HOST=backup-server-01
```

## Security

### RESTIC_INSECURE_NO_PASSWORD
Allow empty password (equivalent to --insecure-no-password).

```bash
export RESTIC_INSECURE_NO_PASSWORD=1
```

### RESTIC_INSECURE_TLS
Skip TLS certificate verification (equivalent to --insecure-tls).

```bash
export RESTIC_INSECURE_TLS=1
```

### RESTIC_CACERT
Path to CA certificate file for HTTPS connections.

```bash
export RESTIC_CACERT=/etc/ssl/certs/ca-certificates.crt
```

### RESTIC_TLS_CLIENT_CERT
Path to PEM-encoded TLS client certificate and private key.

```bash
export RESTIC_TLS_CLIENT_CERT=/path/to/client.pem
```

### RESTIC_HTTP_USER_AGENT
User agent string for HTTP requests.

```bash
export RESTIC_HTTP_USER_AGENT="restic-backup/1.0"
```

## Locking

### RESTIC_RETRY_LOCK
Retry duration when repository is locked.

```bash
# Examples: 1m, 30s, 2h
export RESTIC_RETRY_LOCK=5m
```

## Debugging

### RESTIC_DEBUG
Enable debug output.

```bash
export RESTIC_DEBUG=1
# Or for more verbose
export RESTIC_DEBUG=2
```

### RUST_LOG
Rust logging level (for development builds).

```bash
export RUST_LOG=restic=debug
export RUST_LOG=backtrace=1
```

## Other Options

### RESTIC_BACKEND_RETRY
Maximum number of retries for backend operations.

```bash
export RESTIC_BACKEND_RETRY=5
```

### RESTIC_UPLOAD_QUEUE_SIZE
Size of upload queue (default: 20).

```bash
export RESTIC_UPLOAD_QUEUE_SIZE=50
```

### TMPDIR
Temporary directory for restic operations.

```bash
export TMPDIR=/tmp/restic-temp
```
