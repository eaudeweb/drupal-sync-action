# Synchronize two Drupal instances

Caveat: At the moment only the database is synchronized.

## Usage

```yml
steps:
  - uses: actions/checkout@v3

  - uses: eaudeweb/drupal-sync-action@2.x
    with:
      target_ssh_user:             ${{ secrets.TEST_SSH_USER }}
      target_ssh_host:             ${{ secrets.TEST_SSH_HOST }}
      target_ssh_key:              ${{ secrets.TEST_SSH_KEY }}
      target_project_dir:          /var/www/html/www.example.com
```