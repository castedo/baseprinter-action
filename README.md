# Baseprinter Action

This is a reusable automation workflow for [GitHub Actions](https://github.com/features/actions)
that runs [Baseprinter](https://try.perm.pub/baseprinter) to generate a Baseprint
document snapshot and commit it to a branch named `autobaseprint`.
This reusable workflow is also useful for automatically generating an HTML/PDF preview
website.


## Quick Start

To quickly get started, use
[`baseprint-starter`](https://github.com/castedo/baseprint-starter/)
as a template to [create a new repository](
https://github.com/new?template_owner=castedo&template_name=baseprint-starter
).

Alternatively, use the contents of
[`baseprint-starter`](https://github.com/castedo/baseprint-starter/) as an example.


## Inputs

### `just-recipe`

Default value: `baseprint`.

This input parameter specifies the [just](https://just.systems) recipe to run.

An example [just](https://just.systems) recipe is in
[`justfile` in `baseprint-starter`](
https://github.com/castedo/baseprint-starter/blob/main/justfile
).

### `baseprint-path`

Default value: `baseprint`.

Do not use this path in sources.
Baseprinter will generate baseprint snapshot contents into the path assigned to
`baseprint-path`.
This path will be automatically committed and pushed to the `autobaseprint` branch.
