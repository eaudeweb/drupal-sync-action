# Synchronize Drupal database between instances

Downloads a database dump from Nextcloud and restores it on the target Drupal instance.

## Usage

```yml
on:
  workflow_dispatch:

name: 'Sync PRODUCTION to TEST'
jobs:
  db:
    name: 'Executing synchronization'
    runs-on: ${{ vars.TEST_RUNNER || 'drupal-runner-v2' }}
    steps:
      - name: 'Running'
        uses: eaudeweb/drupal-sync-action@2.x
        with:
          target_ssh_user:             ${{ secrets.TEST_SSH_USER }}
          target_ssh_host:             ${{ secrets.TEST_SSH_HOST }}
          target_ssh_key:              ${{ secrets.TEST_SSH_KEY }}
          target_project_dir:          ${{ vars.TEST_PROJECT_DIR }}
          nextcloud_path:              ${{ vars.PROD_NEXTCLOUD_PATH }}
          nextcloud_user:              ${{ secrets.NEXTCLOUD_USER }}
          nextcloud_app_password:      ${{ secrets.NEXTCLOUD_APP_PASSWORD }}
```
