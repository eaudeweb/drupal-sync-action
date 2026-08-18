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

## Unblocking accounts after the import

The dump carries the account status from the source instance, so users blocked in
production land blocked on the target. Pass a comma delimited list of user names
to `unblock_users` and the action runs `drush user:unblock` on them once the
import finishes:

```yml
          unblock_users:               ${{ vars.TEST_UNBLOCK_USERS }}
```

Keeping the list in a repository variable means adding or removing an account
does not require changing the workflow. The step is skipped when the input is
empty, and when `sync_db` is `false`.
