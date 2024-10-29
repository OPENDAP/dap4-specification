# DAP4 Specification

This repository serves two greater purposes:

- Stores the source files, and builds and deploys the [Official Documentation for the DAP4 Specification](https://opendap.github.io/dap4-specification/DAP4.html). 

- Space for greater discussions on the DAP4 specification between developers from Unidata and OPeNDAP, Inc. For this, we refer the issue tracker.


## Instructions for adding to the documentation

The documentation is built automatically from the source `AsciiDoc` files (`*.adoc`). To propose any change you need to create a new branch, and submit a PR with the proposed changes for review. Before submitting a new PR, we suggest to tryout to build the documentation on a local machine.


### Minimal Requirements for testing locally
To build the documentation (`html`) locally, is to have installed
- AsciiDoctor
- Clone the Repository

### Instructions
- Optional: Navigate to the root directory. `DAP4.adoc` should be there.
- Make changes (using a new branch - do not commit on `main`).
- Test the proposed changes by running the command:
```
asciidoctor -a toc=left -a docinfo=shared DAP4.adoc
````
- The command above should generate a new file `DAP4.html`. You can inspect it with a brower, e.g. `open DAP4.html`.
- Add and commit the new changes, and push to Request a `Pull Request` review. Once approved, the changes should be published automatically by `Travis`.

