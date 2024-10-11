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

## License

Copyright 2024 gematik GmbH

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in
compliance with the License.

See the [LICENSE](./LICENSE) for the specific language governing permissions and limitations under
the License.

Unless required by applicable law the software is provided "as is" without warranty of any kind,
either express or implied, including, but not limited to, the warranties of fitness for a particular
purpose, merchantability, and/or non-infringement. The authors or copyright holders shall not be
liable in any manner whatsoever for any damages or other claims arising from, out of or in connection
with the software or the use or other dealings with the software, whether in an action of contract,
tort, or otherwise.

The software is the result of research and development activities, therefore not necessarily quality
assured and without the character of a liable product. For this reason, gematik does not provide any
support or other user assistance (unless otherwise stated in individual cases and without justification
of a legal obligation). Furthermore, there is no claim to further development and adaptation of the
results to a more current state of the art.

Gematik may remove published results temporarily or permanently from the place of publication at any
time without prior notice or justification.
