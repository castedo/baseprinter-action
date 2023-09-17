# Basecast action

This is a reusable automation workflow for [GitHub Actions](https://github.com/features/actions)
that generates and deploys baseprints and HTML/PDF previews using
[basecast](https://baseprints.singlesource.pub/basecast).


## Inputs

The `defaults-file` input parameter is required.
It specifies the path to the location of a
pandoc defaults file (relative to the repository).
A pandoc defaults file can specify the input source files.


## Quick Start

The quickest way to get started is to use
[basecastbot-example](https://github.com/castedo/basecastbot-example/)
as a template to [create a new repository](
https://github.com/new?template_owner=castedo&template_name=basecastbot-example
).

Alternatively, just add a workflow file, such as
[basecastbot-example .github/workflows/pages-deploy.yaml](
https://github.com/castedo/basecastbot-example/blob/main/.github/workflows/pages-deploy.yaml
)
or the example below,
to an existing repository.


## Example usage

The following is an example of a workflow YAML file that can be placed at
`.github/workflows/basecastbot.yaml`.
This workflow will generate a baseprint and deploy an HTML/PDF preview to GitHub Pages.

```yaml
name: Deploy baseprint preview to GitHub Pages

on:
  push:
    branches: [$default-branch]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Grant GITHUB_TOKEN the permissions required to make a Pages deployment
permissions:
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-22.04
    steps:
      - uses: castedo/basecast-build-action@v1
        with:
          defaults-file: "pandocin.yaml"
  deploy:
    needs: build
    runs-on: ubuntu-22.04
    steps:
      - name: "Deploy to GitHub Pages"
        id: deployment
        uses: actions/deploy-pages@v1
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
```
