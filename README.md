# Shuttle Deploy Action

This action automates the deployment of a Rust project to [Shuttle](https://www.shuttle.dev/). This action deploys the project to Shuttle, which builds it and hosts it.

Note that you need to have created a project on Shuttle before you can deploy to it. Provide the project ID in the inputs.

**Shuttle Secrets** are saved from previous deployments. Therefore, they are usually not be needed in your CD pipeline.
The choice is yours, whether you prefer to add **Shuttle Secrets** with a manual deployment, or in a continuous way using the `secrets` input of this action.
Read more about **Shuttle Secrets** [here](https://docs.shuttle.dev/resources/shuttle-secrets).

## Inputs

| Name                  | Description | Required | Default |
|-----------------------| --- | --- | --- |
| shuttle-api-key       | The Shuttle API key | true | N/A |
| project-id            | Project ID, starts with `proj_` | true | N/A |
| cargo-shuttle-version | Version of cargo-shuttle | false | `""` (latest) |
| working-directory     | The cargo workspace root | false | `"."` |
| secrets               | Content of the `Secrets.toml` file, if any | false | `""` |
| extra-args            | Extra args to the deploy command | false | `""` |

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
      - uses: shuttle-hq/deploy-action@v2
        with:
          shuttle-api-key: ${{ secrets.SHUTTLE_API_KEY }}
          project-id: proj_0123456789
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
      - uses: shuttle-hq/deploy-action@v2
        with:
          shuttle-api-key: ${{ secrets.SHUTTLE_API_KEY }}
          project-id: proj_0123456789
          working-directory: "backend"
          cargo-shuttle-version: "0.48.1"
          extra-args: --allow-dirty --debug
          secrets: |
            MY_AWESOME_SECRET_1 = '${{ secrets.SECRET_1 }}'
            MY_AWESOME_SECRET_2 = '${{ secrets.SECRET_2 }}'
```
