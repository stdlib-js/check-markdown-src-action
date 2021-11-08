<!--

@license Apache-2.0

Copyright (c) 2021 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->

# Check HTML `src` Attributes

> A GitHub action to check all HTML `src` attributes in the Markdown files of a directory.

## Example Workflow

```yml
# Workflow name:
name: Check HTML `src` attributes in the Markdown files of a directory

# Workflow triggers:
on:
  push:

# Workflow jobs:
jobs:
  check_markdown_links:
    # Define the type of virtual host machine on which to run the job:
    runs-on: ubuntu-latest

    # Define the sequence of job steps...
    steps:
      # Checkout the current branch:
      - uses: actions/checkout@v2
      # Run the command to check Markdown links:
      - id: check-links
        uses: stdlib-js/check-markdown-src-action@v1.0
        with:
          directory: fixtures
      # Print out the results:
      - run: |
          echo ${{ steps.check-links.outputs.links }}
          echo Status: ${{ steps.check-links.outputs.status }}
      # Fail the workflow if the status is not "success":
      - if: ${{ steps.check-links.outputs.status }} != 'success'
        run: |
          exit 1
```


## Inputs

-   `directory` (string) : directory containing Markdown files to recursively check URL `src` attributes.
-   `exclude` (string) : regular expression pattern for `src` attributes that should be skipped. 
-   `successCodes` (array of integers) : array of HTTP status codes that should be considered a success. Defaults to `[200, 201, 202, 203, 204, 205, 206, 207, 208, 226]`.
-   `warningCodes` (array of integers) : array of HTTP status codes that should be considered a warning. Defaults to `[300, 301, 302, 303, 304, 305, 306, 307, 308]`.


## Outputs 

-  `failures` (JSON object array): array of JSON objects for `src` URLs considered broken containing the following properties:
    -   `url` (string) : broken link.
    -   `code` (number) : HTTP status code received for the broken link.
    -   `status` (string) : description of the HTTP status code.
    -   `file` (string) : path to the Markdown file that contains the broken URL definition.
-  `warnings` (JSON object array): array of JSON objects for `src` URLs triggering warnings containing the following properties:
    -   `url` (string) : link triggering warning.
    -   `code` (number) : HTTP status code received for the link.
    -   `status` (string) : description of the HTTP status code.
    -   `file` (string) : path to the Markdown file that contains the URL definition.
-  `status` (string): Status of the job (`success` or `failure`).


## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2021. The Stdlib [Authors][stdlib-authors].

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/check-markdown-src-action/main/LICENSE

</section>

<!-- /.links -->
