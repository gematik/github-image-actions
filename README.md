github-image-actions
====================

A collection of GitHub actions for processing images.

## Actions

### lint-asciidoc

Verifies that:

- `.adoc` files don't contain image macros that reference dead links or non-existing files
- `.adoc` files don't contain `<img>` tags (because the action cannot verify them as easily)

```yaml
jobs:
  lint
    runs-on: ubuntu-latest

    steps:
      - name: Check out repository
        uses: actions/checkout@v4

      - name: Lint
        uses: gematik/github-image-actions/.github/actions/lint-asciidoc@...
```

### lint-drawio

Verifies that:

- `.drawio` files don't contain more than a single diagram (because bulk-exporting multiple pages isn't supported)

```yaml
jobs:
  lint
    runs-on: ubuntu-latest

    steps:
      - name: Check out repository
        uses: actions/checkout@v4

      - name: Lint
        uses: gematik/github-image-actions/.github/actions/lint-drawio@...
```

### lint-plantuml

Verifies that:

- `.puml` files don't contain inline file names (because these override the output file name specified during exporting)

```yaml
jobs:
  lint
    runs-on: ubuntu-latest

    steps:
      - name: Check out repository
        uses: actions/checkout@v4

      - name: Lint
        uses: gematik/github-image-actions/.github/actions/lint-plantuml@...
```

## Workflows

### generate-images

Exports PNGs and SVGs from `.drawio` and `.plantuml` files and commits them into the repository.

```yaml
jobs:
  generate:
    uses: gematik/github-image-actions/.github/workflows/generate-images.yml@...
    with:
      srcdir: src/images
      outdir: images/generated
      ref: ...
```

```yaml
inputs:
  srcdir:
    required: true
    type: string
    description: Relative path to the directory in which to search for .drawio and .puml source files
  outdir:
    required: true
    type: string
    description: Relative path to the directory in which to write the .png and .svg output files
  ref:
    required: true
    type: string
    description: The GitHub ref to use for local actions (should normally be the same ref that this workflow is called on)
```
