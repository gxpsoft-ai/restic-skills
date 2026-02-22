# Restic Commands Reference

## Initialization

### `restic init`
Initialize a new repository. Creates the repository structure and encryption keys.

```bash
restic init
# Or with explicit backend
restic init --repo /srv/restic-repo
restic init --backend sftp --host user@backupserver:/path
```

## Backup Commands

### `restic backup`
Create a new backup snapshot.

```bash
# Basic backup
restic backup /path/to/files

# Multiple paths
restic backup ~/Documents ~/Pictures

# With exclude patterns
restic backup /data --exclude "*.tmp" --exclude ".git"

# From file list
restic backup --files-from /path/to/file-list

# Dry run
restic backup /data --dry-run

# With tags
restic backup /data --tag "daily-backup"

# From stdin
echo "/path" | restic backup --stdin

# From command
restic backup --stdin-from-command -- /bin/ls -la

# Backup to specific host
restic backup /data --host myserver

# With parent snapshot
restic backup /data --parent latest-snapshot-id
```

### `restic snapshots`
List all snapshots.

```bash
# List all snapshots
restic snapshots

# JSON output
restic snapshots --json

# Filter by host
restic snapshots --host myserver

# Filter by path
restic snapshots --path /data

# Filter by tags
restic snapshots --tag daily-backup

# Group by
restic snapshots --group-by host,paths
```

### `restic ls`
List files in a snapshot.

```bash
# List files in latest snapshot
restic ls latest

# List files in specific snapshot
restic ls abc123

# Long format with metadata
restic ls -l latest

# Recursive
restic ls -R latest

# JSON output
restic ls --json latest
```

### `restic diff`
Show differences between two snapshots.

```bash
# Compare two snapshots
restic diff abc123 def456

# Compare with latest
restic diff latest abc123
```

## Restore Commands

### `restic restore`
Restore files from a snapshot.

```bash
# Restore to target directory
restic restore latest --target /tmp/restore

# Restore specific snapshot
restic restore abc123 --target /tmp/restore

# Restore specific path
restic restore latest --target /tmp/restore --path /data/files

# Match pattern
restic restore latest --target /tmp/restore --include "*.txt"

# Exclude patterns
restic restore latest --target /tmp/restore --exclude "*.log"
```

### `restic mount`
Mount repository as a filesystem.

```bash
# Mount at mountpoint
restic mount /mnt/restic

# Allow other users
restic mount --allow-other /mnt/restic

# Read-only mount
restic mount -o ro /mnt/restic
```

### `restic dump`
Print backed-up file to stdout.

```bash
# Dump file to stdout
restic dump latest --path /data/file.txt > file.txt

# Dump to stdout directly
restic dump abc123 /data/file.txt
```

## Repository Management

### `restic check`
Check repository for errors.

```bash
# Basic check
restic check

# Full data check
restic check --read-data

# With recovery
restic check --recover
```

### `restic prune`
Remove unused data from repository.

```bash
# Prune unused data
restic prune

# Dry run
restic prune --dry-run

# Max pack size
restic prune --max-pack-size 64
```

### `restic forget`
Remove snapshots according to retention policy.

```bash
# Remove single snapshot
restic forget abc123

# Keep last 7 daily snapshots
restic forget --keep-daily 7

# Keep last 4 weekly snapshots
restic forget --keep-weekly 4

# Keep last 6 monthly snapshots
restic forget --keep-monthly 6

# Keep last 3 yearly snapshots
restic forget --keep-yearly 3

# Keep snapshots with specific tags
restic forget --tag important --keep-tag important

# Prune after forget
restic forget --prune --keep-daily 7
```

### `restic copy`
Copy snapshots between repositories.

```bash
# Copy to another repo
restic copy --repo2 /backup-repo latest

# Copy specific snapshot
restic copy --repo2 /backup-repo abc123
```

### `restic list`
List objects in repository.

```bash
# List all blobs
restic list blobs

# List all packs
restic list packs

# List all snapshots
restic list snapshots

# List all index files
restic list indexes
```

### `restic cat`
Print internal objects.

```bash
# Print blob
restic cat blob abc123

# Print index
restic cat index abc123

# Print snapshot
restic cat snapshot abc123

# Print tree
restic cat tree abc123
```

### `restic find`
Find files in snapshots.

```hello
# Find file by name
restic find file.txt

# Find in all snapshots
restic find --snapshots latest file.txt

# Find by content
restic find --content "pattern"

# Find multiple patterns
restic find "*.txt" "*.doc"
```

### `restic stats`
Show repository statistics.

```bash
# Basic stats
restic stats

# Stats for specific snapshot
restic stats abc123

# Show size in JSON
restic stats --json

# Mode
restic stats --mode restore-size  # or blobs-per-file
```

### `restic key`
Manage repository keys.

```bash
# List keys
restic key list

# Add new key
restic key add

# Remove key
restic key remove abc123

# Show key info
restic key passwd abc123  # change password
```

### `restic tag`
Modify tags on snapshots.

```bash
# Add tag
restic tag latest --tag backup

# Remove tag
restic tag latest --remove-tag old-tag

# Set tags (replace all)
restic tag latest --tag "tag1,tag2"
```

### `restic unlock`
Remove locks from other processes.

```bash
# Remove all locks
restic unlock

# Remove specific lock
restic unlock abc123
```

### `restic migrate`
Apply migrations.

```bash
# List available migrations
restic migrate --list

# Run migration
restic migrate upgrade-repo
```

### `restic recover`
Recover data from corrupted repository.

```bash
# Recover repository
restic recover

# With new repository
restic recover --repo /new-repo
```

### `restic repair`
Repair repository.

```bash
# Repair index
restic repair index

# Repair snapshots
restic repair snapshots

# Repair packs
restic repair packs
```

### `restic rewrite`
Rewrite snapshots to exclude unwanted files.

```bash
# Rewrite to exclude patterns
restic rewrite --exclude "*.log" latest

# Dry run
restic rewrite --dry-run --exclude "*.tmp" latest
```

## Cache Management

### `restic cache`
Operate on local cache.

```bash
# List cache location
restic cache

# List cached items
restic cache --list

# Clear cache
restic cache --clear

# Clear for specific repo
restic cache --clear --repo /my-repo
```

## System

### `restic self-update`
Update restic binary.

```bash
# Update to latest version
restic self-update

# Install specific version
restic self-update 0.16.0

# Check version
restic version
```

### `restic generate`
Generate manual pages and auto-completion.

```bash
# Generate bash completion
restic generate --bash-completion

# Generate zsh completion
restic generate --zsh-completion

# Generate fish completion
restic generate --fish-completion

# Generate man pages
restic generate --man-page /tmp/man
```

### `restic features`
Print available feature flags.

```bash
restic features --json
```

### `restic options`
Print extended options.

```bash
restic options
```

## Global Flags

```bash
-r, --repo REPO              Repository location
-p, --password-file FILE     Password file
--password-command COMMAND   Command to get password
--json                       JSON output
-q, --quiet                  Quiet mode
-v, --verbose                Verbose (can be -v, -vv)
--no-cache                   Don't use cache
--cache-dir DIR              Cache directory
--cacert FILE                CA certificate
--tls-client-cert FILE       TLS client certificate
--insecure-no-password       Empty password
--insecure-tls               Skip TLS verification
-o, --option KEY=VALUE       Extended option
--limit-download RATE        Download limit (KiB/s)
--limit-upload RATE          Upload limit (KiB/s)
--pack-size SIZE             Pack size (MiB)
--compression MODE           Compression (auto|off|max)
-h, --help                   Help
```
