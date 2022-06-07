# Shuttle deploy action

Deploys current project to [shuttle.rs](https://www.shuttle.rs)

Will checkout the repository if not already checked out

### Inputs

`deploy-key`, the key found at https://www.shuttle.rs/login

`working-directory`, the directory which includes the `Cargo.toml`, **defaults to `"."`**

`allow-dirty`, allow uncommitted changes to be deployed, **defaults to `"false"`**

### Outputs

None

### Example usage

```yml
name: Shuttle deploy

on:
  push:
    branches:
      - "main"

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: shuttle-hq/deploy-action@main
        with:
          deploy-key: ${{ secrets.SHUTTLE_DEPLOY_KEY }}
```