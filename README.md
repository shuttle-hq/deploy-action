# Shuttle Deploy Action

This action automates the deployment of a rust project to [Shuttle](https://www.shuttle.rs/). This action builds the project and then deploys the result to Shuttle.

Note that you need to have created a project on Shuttle before you can deploy to it. This action will NOT create a new project for you.
You can see the documentation on how to create a project [here](https://docs.shuttle.rs/introduction/quick-start).

## Inputs

| Name | Description | Required | Default |
| --- | --- | --- | --- |
| deploy-key | The Shuttle API key | true | N/A |
| working-directory | The directory which includes the `Cargo.toml` | false | `"."` |
| allow-dirty | Allow uncommitted changes to be deployed | false | `"false"` |

## Outputs

| Name | Description |
| --- | --- |
| shuttle-url | The URL of the deployed project |

## Example usage

### Typical Example

```yaml
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

### Example with all inputs

```yaml
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
          working-directory: "my-project"
          allow-dirty: "true"
```
