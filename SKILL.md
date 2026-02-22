---
name: restic
description: Restic is a fast, secure, and free backup program. This skill provides comprehensive knowledge of restic documentation for backing up, restoring, and managing encrypted backups across various storage backends.
references:
  - references/commands.md
  - references/backends.md
  - references/environment_variables.md
---

# Restic - Fast, Secure Backup Program

Restic is a backup program that allows saving multiple revisions of files and directories in an encrypted repository stored on different backends.

## Quick Start

```bash
# Set environment variables
export RESTIC_REPOSITORY=/srv/restic-repo
export RESTIC_PASSWORD=some-strong-password

# Initialize repository (first time only)
restic init

# Create backup
restic backup ~/work

# List snapshots
restic snapshots

# Restore backup
restic restore --target /tmp/restore-work your-snapshot-ID

# Check repository
restic check
```

## Core Commands

- `restic init` - Initialize a new repository
- `restic backup` - Create a new backup snapshot
- `restic restore` - Restore files from a snapshot
- `restic snapshots` - List all snapshots
- `restic ls` - List files in a snapshot
- `restic diff` - Show differences between snapshots
- `restic check` - Verify repository integrity
- `restic forget` - Remove snapshots according to retention policy
- `restic prune` - Remove unused data from repository
- `restic mount` - Mount repository as a filesystem
- `restic cat` - Print internal objects
- `restic copy` - Copy snapshots between repositories
- `restic find` - Find files in snapshots
- `restic dump` - Print backed-up file to stdout
- `restic key` - Manage repository keys
- `restic list` - List objects in repository
- `restic migrate` - Apply migrations
- `restic recover` - Recover data from corrupted repository
- `restic repair` - Repair repository
- `restic rewrite` - Rewrite snapshots to exclude files
- `restic stats` - Show repository statistics
- `restic tag` - Modify tags on snapshots
- `restic unlock` - Remove locks from other processes
- `restic self-update` - Update restic binary
- `restic version` - Print version information
- `restic cache` - Operate on local cache
- `restic features` - Print feature flags
- `restic options` - Print extended options
- `restic generate` - Generate manual pages and auto-completion

## Documentation Structure

### Installation
- Packages for: Alpine, Arch, Debian, Fedora, Gentoo, macOS (Homebrew)
- Official binaries for all major platforms
- Docker container
- Build from source
- Autocompletion for bash, fish, zsh, PowerShell

### Repository Backends
- **Local** - Filesystem storage
- **SFTP** - SSH file transfer
- **REST Server** - HTTP REST API
- **Amazon S3** - AWS S3
- **Minio Server** - Self-hosted S3-compatible
- **S3-compatible Storage** - Any S3-compatible service
- **Wasabi** - Wasabi cloud storage
- **Alibaba Cloud OSS** - Aliyun Object Storage
- **OpenStack Swift** - Swift object storage
- **Backblaze B2** - Backblaze B2 cloud storage
- **Microsoft Azure Blob Storage** - Azure storage
- **Google Cloud Storage** - Google Cloud Storage
- **rclone** - Any rclone-supported backend

### Backup Features
- File change detection
- Skip unchanged snapshots
- Dry run mode
- Exclude/include files with patterns
- Compare snapshots
- Backup special items and metadata
- Read from stdin
- Tags for organization
- Scheduling integration (cron, systemd)
- Exit status codes for scripting

### Repository Management
- Listing snapshots
- Copying snapshots between repos
- Removing files from snapshots
- Modifying metadata
- Checking integrity
- Upgrading repository format

### Performance Tuning
- Disable backup progress estimation
- Backend connections (parallel connections)
- CPU usage (compression, crypto)
- Compression modes (auto/off/max)
- Data verification
- File read concurrency
- Pack size configuration
- Feature flags

### Security
- AES-256 encryption
- Authenticated encryption
- Key management (multiple keys per repo)
- Secure password handling

### Scripting
- JSON output for all commands
- Exit codes
- Environment variables
- Password command execution

### Troubleshooting
- Find damaged data
- Backup repository
- Repair index
- Remove missing data from snapshots

## Environment Variables

Key environment variables:
- `RESTIC_REPOSITORY` - Repository location
- `RESTIC_PASSWORD` - Repository password
- `RESTIC_PASSWORD_FILE` - File containing password
- `RESTIC_PASSWORD_COMMAND` - Command to get password
- `RESTIC_KEY_HINT` - Key ID to try first
- `RESTIC_CACHE_DIR` - Cache directory
- `RESTIC_COMPRESSION` - Compression mode
- `RESTIC_READ_CONCURRENCY` - File read concurrency
- `RESTIC_PACK_SIZE` - Target pack size
- `RESTIC_PROGRESS_FPS` - Progress reporting frequency
- `RESTIC_HOST` - Hostname for snapshot
- `RESTIC_CACERT` - CA certificate file

## Common Options

- `-r, --repo` - Repository location
- `-p, --password-file` - Password file
- `--password-command` - Password command
- `-o, --option` - Extended options
- `--json` - JSON output
- `-q, --quiet` - Quiet mode
- `-v, --verbose` - Verbose output
- `--no-cache` - Disable cache
- `--insecure-no-password` - Empty password
- `--insecure-tls` - Skip TLS verification

## Related Documentation

- [Commands Reference](references/commands.md) - Detailed command documentation
- [Backend Storage](references/backends.md) - All storage backend configurations
- [Environment Variables](references/environment_variables.md) - Complete environment variable reference
