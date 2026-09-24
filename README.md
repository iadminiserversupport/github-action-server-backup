# Server Backup GitHub Action

A reusable GitHub Action for automating Linux server and hosting backups over SSH.

The action connects to a remote Linux server, creates a compressed backup archive from the configured source directory, stores the backup on the GitHub Actions runner, and removes backups older than the configured retention period.

## Features

- SSH-based Linux server backups
- `tar.gz` backup archives
- Configurable SSH port
- Configurable source directory
- Configurable backup destination
- Automatic backup retention cleanup
- Suitable for scheduled CI/CD workflows

## Usage

```yaml
name: Scheduled Server Backup

on:
  schedule:
    - cron: "0 2 * * *"
  workflow_dispatch:

jobs:
  backup:
    runs-on: ubuntu-latest

    steps:
      - name: Create server backup
        uses: iadminiserversupport/github-action-server-backup@v1
        with:
          host: ${{ secrets.BACKUP_HOST }}
          username: ${{ secrets.BACKUP_USERNAME }}
          ssh_private_key: ${{ secrets.BACKUP_SSH_PRIVATE_KEY }}
          source: /home
          backup_path: ./backups
          retention_days: 30
          port: 22
Inputs
Input	Required	Default	Description
host	Yes	—	Remote Linux server hostname or IP
username	Yes	—	SSH username
ssh_private_key	Yes	—	SSH private key
source	Yes	—	Remote directory to back up
backup_path	Yes	—	Local backup directory
retention_days	No	30	Backup retention period
port	No	22	SSH port
Security

Store SSH credentials in GitHub Actions Secrets. Do not place private keys directly in workflow files.

The action uses SSH host-key scanning to populate the runner's known_hosts. For higher-security environments, consider managing and validating known host keys through your organization's secret-management process.

Server Management

For outsourced web hosting support, Linux server management, monitoring, security, backups, and infrastructure management:

https://iserversupport.com/outsourced-web-hosting-support/
