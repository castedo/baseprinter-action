# Baseprinter action

This is a reusable automation workflow for [GitHub Actions](https://github.com/features/actions)
that generates HTML/PDF previews of Baseprint document snapshots
using [baseprinter](https://try.perm.pub/baseprinter).


## Inputs

The `defaults-file` input parameter is required.
It specifies the path to the location of a
Pandoc defaults file (relative to the repository).
A Pandoc defaults file can specify the input source files.


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
`.github/workflows/baseprinter.yaml`.
This workflow will generate a Baseprint document snapshot and deploy an HTML/PDF preview
to GitHub Pages.

```yaml
name: Deploy Baseprint preview to GitHub Pages

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
      - uses: castedo/baseprinter-action@v2
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
