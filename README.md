github-image-actions
====================

A collection of GitHub actions for processing images.

# Actions

## lint-asciidoc

Verifies that:

- `.adoc` files don't contain image macros that reference dead links or non-existing files
- `.adoc` files don't contain `<img>` tags (because the action cannot verify them as easily)

```
jobs:
  lint
    runs-on: ubuntu-latest

    steps:
      - name: Check out repository
        uses: actions/checkout@v4

      - name: Lint
        uses: gematik/github-image-actions/.github/actions/lint-asciidoc@...
```

## lint-drawio

Verifies that:

- `.drawio` files don't contain more than a single diagram (because bulk-exporting multiple pages isn't supported)

```
jobs:
  lint
    runs-on: ubuntu-latest

    steps:
      - name: Check out repository
        uses: actions/checkout@v4

      - name: Lint
        uses: gematik/github-image-actions/.github/actions/lint-drawio@...
```

## lint-plantuml

Verifies that:

- `.puml` files don't contain inline file names (because these override the output file name specified during exporting)

```
jobs:
  lint
    runs-on: ubuntu-latest

    steps:
      - name: Check out repository
        uses: actions/checkout@v4

      - name: Lint
        uses: gematik/github-image-actions/.github/actions/lint-plantuml@...
```
