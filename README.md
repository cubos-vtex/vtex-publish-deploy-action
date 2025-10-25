# vtex-publish-deploy-action
An action than publishes and deploys a VTEX IO app after release

## Requirements
First, you need to create an [application key](https://help.vtex.com/pt/tutorial/chaves-de-aplicacao--2iffYzlvvz4BDMr6WGUtet) with publish, install and deploy app permissions for your account.

Then, create the following secrets in your [Github repository secrets](https://docs.github.com/pt/actions/security-guides/using-secrets-in-github-actions) with respectively values of created application key and token:
- `VTEX_TOOLBELT_KEY`
- `VTEX_TOOLBELT_TOKEN`

## How to use
Simply create a yml file under `.github/workflows` directory of your project with the suggested content:

```yml
name: Publish and Deploy App

on:
  push:
    tags:
      - "v[0-9]+.[0-9]+.[0-9]+"
  workflow_dispatch:

jobs:
  publish_and_deploy:
    permissions:
      contents: write
    name: Publish and Deploy App
    runs-on: ubuntu-latest
    steps:
      - uses: cubos-vtex/vtex-publish-deploy-action@v9
        with:
          appKey: ${{ secrets.VTEX_TOOLBELT_KEY }}
          appToken: ${{ secrets.VTEX_TOOLBELT_TOKEN }}
```

Then, after each `vtex release patch|minor|major stable` command, where a tag with `v[0-9]+.[0-9]+.[0-9]+` pattern is created in the repository, the action will be executed.
