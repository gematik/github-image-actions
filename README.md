<img align="right" width="250" height="47" src="gematik.png"/>

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
    description: Relative path to the directory in which to write the generated output files
  ref:
    required: true
    type: string
    description: The GitHub ref to use for local actions (should normally be the same ref that this workflow is called on)
  png:
    required: false
    default: true
    type: boolean
    description: Whether to generate PNG images from the source files
  svg:
    required: false
    default: true
    type: boolean
    description: Whether to generate SVG images from the source files
```

## License

Copyright 2024-2025 gematik GmbH

Apache License, Version 2.0

See the [LICENSE](./LICENSE) for the specific language governing permissions and limitations under the License

## Additional Notes and Disclaimer from gematik GmbH

1. Copyright notice: Each published work result is accompanied by an explicit statement of the license conditions for use. These are regularly typical conditions in connection with open source or free software. Programs described/provided/linked here are free software, unless otherwise stated.
2. Permission notice: Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
    1. The copyright notice (Item 1) and the permission notice (Item 2) shall be included in all copies or substantial portions of the Software.
    2. The software is provided "as is" without warranty of any kind, either express or implied, including, but not limited to, the warranties of fitness for a particular purpose, merchantability, and/or non-infringement. The authors or copyright holders shall not be liable in any manner whatsoever for any damages or other claims arising from, out of or in connection with the software or the use or other dealings with the software, whether in an action of contract, tort, or otherwise.
    3. The software is the result of research and development activities, therefore not necessarily quality assured and without the character of a liable product. For this reason, gematik does not provide any support or other user assistance (unless otherwise stated in individual cases and without justification of a legal obligation). Furthermore, there is no claim to further development and adaptation of the results to a more current state of the art.
3. Gematik may remove published results temporarily or permanently from the place of publication at any time without prior notice or justification.
4. Please note: Parts of this code may have been generated using AI-supported technology. Please take this into account, especially when troubleshooting, for security analyses and possible adjustments.
