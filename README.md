# Installation

This project is run using `docker-compose` to orchestrate the Docker containers.

### Service Account

- Log into the [GCP IAM console](https://console.cloud.google.com/iam-admin/serviceaccounts?authuser=2&cloudshell=true&project=chris-esplin)
- Create a service account with the `roles/storage.objectAdmin`, a.k.a. _Storage Object Admin_ permissions
- Create a `json` key and download it.
- Copy your `*.json` key to `./dev/vault/service-account.json`

### GCP Back End

Edit `./dev/vault/vault.config.json and change the`gcs`bucket to a bucket that you own and that is controlled by your`service-account.json`.

# Use with `docker-compose`

### Run All Servers

- Run all servers with `docker-compose up`.
- Run in daemon mode with `dc up -d`. Bring them back down out of daemon mode with `dc down`.
- List running daemons with `docker-compose ps`.

### Run Vault

- Connect to a running `vault` daemon with `docker exec -it vscode-remote-starter_vault_1 sh`.
- Watch daemon logs with `docker-compose logs -f vault`.
- Get shell access to the `vault` container with `sh bin/interactive-vault.sh`.
- Run just Vault with `sh ./bin/run-vault.sh`.
