# Installation

This project is run using `docker-compose` to orchestrate the Docker containers.

### Service Account

- Log into the [GCP IAM console](https://console.cloud.google.com/iam-admin/serviceaccounts?authuser=2&cloudshell=true&project=chris-esplin)
- Create a service account with the `roles/storage.objectAdmin`, a.k.a. _Storage Object Admin_ permissions
- Create a `json` key and download it.
- Copy your `*.json` key to `./dev/vault/service-account.json`

### Environment Variables

Copy `dev/vault/env.list.dist` and get rid of the `.dist` suffix. Fill in the values with whatever you generated from the vault.

If you used more than one key, add them to `env.list` and edit `dev/vault/bin/unseal.sh` to provide the keys to the `vault operator unseal` function.

### GCP Back End

Edit `./dev/vault/vault.config.json` and change the `gcs` bucket to a bucket that you own and that is controlled by your `service-account.json`.

# Docker Compose

### Run All Servers

- Run all servers with `docker-compose up`.
- Run in daemon mode with `docker-compose up -d`.
- Bring daemons down out with `docker-compose down`.
- List running daemons with `docker-compose ps`.

### Run Vault

- Bring up just `vault` in daemon mode with `docker-compose up -d vault`
- Connect to a running `vault` daemon with `docker exec -it vault sh`.
- Watch daemon logs with `docker-compose logs -f vault`.
- Get shell access to the `vault` container with `sh bin/interactive-vault.sh`.
- Run just Vault with `sh ./bin/run-vault.sh`.
- Access the running Vault web UI at [http://localhost:8200/](http://localhost:8200/)

# Extract Secrets

Make sure that `vault` is running with `docker-compose up -d vault`.

Run `sh bin/vault/copy-vault-keys.sh` to extract vault keys and expand secrets to separate files within `./app/vault/`.
