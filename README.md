# Basecast action

This is a reusable automation workflow for [GitHub Actions](https://github.com/features/actions)
that generates and deploys baseprints and HTML/PDF previews using
[basecast](https://baseprints.singlesource.pub/basecast).


## Inputs

The `defaults-file` input parameter is required.
It specifies the path to the location of a
pandoc defaults file (relative to the repository).
A pandoc defaults file can specify the input source files.


## Example usage

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
