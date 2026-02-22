# Restic Skill Builder

Claude Code skill for [restic](https://restic.readthedocs.io/) - a fast, secure, and free backup program.

## Overview

This skill provides comprehensive knowledge of restic for backing up, restoring, and managing encrypted backups across various storage backends. It was built by navigating the official restic documentation using playwright-cli.

## Files

```
restic-skill-builder/
├── SKILL.md                    # Main skill file
├── README.md                   # This file
└── references/
    ├── commands.md             # Complete command reference
    ├── backends.md            # Storage backend configurations
    └── environment_variables.md # Environment variables guide
```

## Quick Start

```bash
# Set environment variables
export RESTIC_REPOSITORY=/srv/restic-repo
export RESTIC_PASSWORD=some-strong-password

# Initialize repository
restic init

# Create backup
restic backup ~/work

# List snapshots
restic snapshots

# Restore backup
restic restore --target /tmp/restore latest

# Check repository
restic check
```

## Supported Backends

- Local filesystem
- SFTP (SSH)
- REST Server
- Amazon S3
- Minio Server
- Wasabi
- Backblaze B2
- Microsoft Azure Blob Storage
- Google Cloud Storage
- Alibaba Cloud OSS
- OpenStack Swift
- Any rclone-supported backend

## Commands Covered

- `backup` - Create new backup snapshots
- `restore` - Restore files from snapshots
- `snapshots` - List all snapshots
- `ls` - List files in snapshots
- `diff` - Compare snapshots
- `check` - Verify repository integrity
- `prune` - Remove unused data
- `forget` - Remove snapshots by policy
- `mount` - Mount repository as filesystem
- `copy` - Copy snapshots between repos
- `key` - Manage encryption keys
- `tag` - Modify snapshot tags
- `find` - Find files in snapshots
- And many more...

## Environment Variables

Key variables:
- `RESTIC_REPOSITORY` - Repository location
- `RESTIC_PASSWORD` - Repository password
- `RESTIC_PASSWORD_FILE` - Password file path
- `RESTIC_PASSWORD_COMMAND` - Command to get password
- `AWS_ACCESS_KEY_ID` / `AWS_SECRET_ACCESS_KEY` - AWS credentials
- `RESTIC_CACHE_DIR` - Cache directory
- And many more...

## Documentation

- [SKILL.md](SKILL.md) - Main skill documentation
- [references/commands.md](references/commands.md) - Detailed command reference
- [references/backends.md](references/backends.md) - Backend storage guide
- [references/environment_variables.md](references/environment_variables.md) - Environment variables

## Source

Documentation: https://restic.readthedocs.io/en/stable/

Version: 0.18.1 (stable)
