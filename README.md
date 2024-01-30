# Shuttle Deploy Action

This action automates the deployment of a Rust project to [Shuttle](https://www.shuttle.rs/). This action deploys the project to Shuttle, which builds it and hosts it.

Note that you need to have created a project on Shuttle before you can deploy to it. This action will NOT create a new project for you.
You can see the documentation on how to create a project [here](https://docs.shuttle.rs/introduction/quick-start).

**Shuttle Secrets** are being saved from previous deployments, therefore, they may be omitted for future deployments.  
The choice is yours, whether you prefer to add **Shuttle Secrets** with a manual deployment, or in a continuous way using the `secrets` input of this action.
Read more about **Shuttle Secrets** [here](https://docs.shuttle.rs/resources/shuttle-secrets).

## Inputs

| Name                  | Description | Required | Default |
|-----------------------| --- | --- | --- |
| deploy-key            | The Shuttle API key | true | N/A |
| cargo-shuttle-version | Version of cargo-shuttle | false | `""` (latest) |
| working-directory     | The directory which includes the `Cargo.toml` | false | `"."` |
| name                  | Override the project name | false | `""` |
| allow-dirty           | Allow uncommitted changes to be deployed | false | `"false"` |
| no-test               | Don't run tests before deployment | false | `"false"` |
| secrets               | Content of the `Secrets.toml` file, if any | false | `""` |
| restart               | Restart project before deployment | false | `"false"` |

## Outputs

| Name | Description |
| --- | --- |
<!-- | shuttle-url | The URL of the deployed project | -->

## Example usage

### Typical Example

```yaml
name: Shuttle Deploy

on:
  push:
    branches:
      - main
  workflow_dispatch:

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: shuttle-hq/deploy-action@main
        with:
          deploy-key: ${{ secrets.SHUTTLE_API_KEY }}
```

### Example with all inputs

```yaml
name: Shuttle Deploy

on:
  push:
    branches:
      - main
  workflow_dispatch:

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: shuttle-hq/deploy-action@main
        with:
          deploy-key: ${{ secrets.SHUTTLE_API_KEY }}
          working-directory: "backend"
          name: "my-project"
          allow-dirty: "true"
          no-test: "true"
          cargo-shuttle-version: "0.28.1"
          restart: "true"
          secrets: |
            MY_AWESOME_SECRET_1 = '${{ secrets.SECRET_1 }}'
            MY_AWESOME_SECRET_2 = '${{ secrets.SECRET_2 }}'
```
