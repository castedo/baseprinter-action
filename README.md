# Baseprinter Action

This is a reusable automation workflow for [GitHub Actions](https://github.com/features/actions)
that generates HTML/PDF previews of Baseprint document snapshots
using [Baseprinter](https://try.perm.pub/baseprinter).


## Inputs

The `defaults-file` input parameter is required.
It specifies the path to a
Pandoc defaults file,
which can specify the input source files.


## Quick Start

To quickly get started, use
[`baseprint-starter`](https://github.com/castedo/baseprint-starter/)
as a template to [create a new repository](
https://github.com/new?template_owner=castedo&template_name=baseprint-starter
).

Alternatively, add a workflow file to an existing repository.
Use [`baseprint-starter .github/workflows/baseprinter.yaml`](
https://github.com/castedo/baseprint-starter/blob/main/.github/workflows/baseprinter.yaml
)
or the following example.


## Example Usage

The following is an example of a workflow YAML file that you can place at
`.github/workflows/baseprinter.yaml`.
This workflow will generate a Baseprint document snapshot and deploy an HTML/PDF preview
to GitHub Pages.

```yaml
name: Deploy Baseprint preview to GitHub Pages

on:
  push:
    branches: [main]

  # Enables manual workflow runs from the Actions tab
  workflow_dispatch:

# Grant necessary permissions for Pages deployment
permissions:
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-22.04
    steps:
      - uses: castedo/baseprinter-action@v3
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
