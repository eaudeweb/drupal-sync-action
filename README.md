# Synchronize two Drupal instances

Caveat: At the moment only the database is synchronized.

## Usage

```yml
on:
  workflow_dispatch:
    inputs:
      sync_db:
        description: 'Synchronize DB'
        type: boolean
        required: true
        default: true
      sync_files:
        description: 'Synchronize "files"'
        type: boolean
        required: true
        default: false

name: 'Sync PRODUCTION to TEST'
jobs:
  db:
    name: 'Executing synchronization'
    runs-on:
      labels: 'drupal'

    steps:
      - name: 'Running'
        uses: eaudeweb/drupal-sync-action@1.x
        with:
          target_ssh_user:             ${{ secrets.TEST_SSH_USER }}
          target_ssh_host:             ${{ secrets.TEST_SSH_HOST }}
          target_ssh_key:              ${{ secrets.TEST_SSH_KEY }}
          target_project_dir:          /var/www/html/example.org
          sync_db: ${{ inputs.sync_db }}
          sync_files: ${{ inputs.sync_files }}
```