# mfe-publish-static-assets-action
This is a GitHub Action meant to be used as a [composite action](https://docs.github.com/en/actions/creating-actions/creating-a-composite-action) within an existing workflow. This action encapsulates setting up a downloads the artifacts from the build process and publishes to S3 in one step. 

The action encapsulates the following other actions:

- [benjlevesque/short-sha](https://github.com/benjlevesque/short-sha)
- [aws-actions/configure-aws-credentials](https://github.com/aws-actions/configure-aws-credentials)
- [actions/download-artifact](https://github.com/actions/download-artifact)



## Inputs

### `aws-access-key-id`

**Required** The associated AWS Secret Key Id for a given AWS Account.

### `aws-secret-access-key`

**Required** The associated AWS Secret Access Key for a given AWS Account. 

### `submodules-pat`

**Required** The PAT Access token required to access the submodules repository.

### `aws-region`

**Required** The PAT Access token required to access the submodules repository.

### `app-name`

**Required** The name of your mfe (e.g. search-mfe, landing-pages-mfe, property-detail-mfe)


## Usage
You can use this composite Action in your own workflow by adding:

```yml
name: search-mfe-composite

on:
  push:
    branches: [ master]

  workflow_dispatch:

jobs:
  publish_static_assets:
    environment: prd
    runs-on: ubuntu-latest
    steps:
      - name: Publish static assets
        uses: awazevr/mfe-publish-static-assets-action@v1.0.1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: eu-west-2
          app-name: search-mfe

```

