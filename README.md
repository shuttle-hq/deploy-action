# Shuttle deploy actions

Deploys current workspace to [shuttle.rs](https://www.shuttle.rs)

Will checkout the repo if not already checked out

### Inputs

`shuttle-deploy-key`, the key found at https://www.shuttle.rs/login

`working-directory`, the folder which includes the project, **defaults to `"."`**

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
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Check source
        run: |
          cargo check
      - uses: shuttle-hq/shuttle-deploy-action@main
        with:
          shuttle-deploy-key: ${{ secrets.SHUTTLE_DEPLOY_KEY }}
```