# Shuttle Deploy Action

This action automates the deployment of a Rust project to [Shuttle](https://www.shuttle.rs/). This action deploys the project to Shuttle, which builds it and hosts it.

Note that you need to have created a project on Shuttle before you can deploy to it. This action will NOT create a new project for you.
You can see the documentation on how to create a project [here](https://docs.shuttle.rs/introduction/quick-start).

Shuttle Secrets are not handled by this action (yet). Add secrets using Secrets.toml with a manual deploy command. Read more about secrets [here](https://docs.shuttle.rs/resources/shuttle-secrets).

## Inputs

| Name                  | Description | Required | Default |
|-----------------------| --- | --- | --- |
| deploy-key            | The Shuttle API key | true | N/A |
| cargo-shuttle-version | Version of cargo-shuttle | false | `""` (latest) |
| working-directory     | The directory which includes the `Cargo.toml` | false | `"."` |
| name                  | The directory which includes the `Cargo.toml` | false | `"."` |
| allow-dirty           | Allow uncommitted changes to be deployed | false | `"false"` |
| idle-minutes          | How long to wait before putting the project in an idle state due to inactivity. 0 means the project will never idle. | false | `"30"` |
| no-test               | Don't run tests before deployment | false | `"false"` |
| secrets               | Content of the `Secrets.toml` file, if any | false | `""` |

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
      - "main"
  workflow_dispatch:

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: shuttle-hq/deploy-action@main
        with:
          deploy-key: ${{ secrets.SHUTTLE_DEPLOY_KEY }}
```

### Example with all inputs

```yaml
name: Shuttle Deploy

on:
  push:
    branches:
      - "main"
  workflow_dispatch:

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: shuttle-hq/deploy-action@main
        with:
          deploy-key: ${{ secrets.SHUTTLE_DEPLOY_KEY }}
          working-directory: "backend"
          name: "my-project"
          allow-dirty: "true"
          idle-minutes: "10"
          no-test: "true"
          cargo-shuttle-version: "0.21.0"
          secrets: |
            MY_AWESOME_SECRET_1 = '${{ secrets.SECRET_1 }}'
            MY_AWESOME_SECRET_2 = '${{ secrets.SECRET_2 }}'
```
