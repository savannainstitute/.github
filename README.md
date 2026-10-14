# Savanna Institute organization defaults

This repository holds the files GitHub applies to every repository in the organization that does
not carry its own copy. `CONTRIBUTING.md` explains, for someone who has never opened a pull request,
how a change gets into a repository. `.github/pull_request_template.md` is the description every
new pull request starts from.

The checks every repository runs, and the templates new repositories start from, are in the
`standards` repository.

## Layout

- `CONTRIBUTING.md`: how to contribute, in plain language. GitHub links to it from every pull
  request page.
- `.github/pull_request_template.md`: the pull request description template.
- `docs/`: every document beyond this file. `docs/adding-a-document.md` says how to add one so the
  tests pass.
- `tests/`: two tests that keep the documents honest. `tests/test_paths.py` checks that every path
  a document names exists and that every link to another file in this repository leads somewhere.
  `tests/test_manifest.py` checks that every JSON file is valid and names only files that exist.

## Running the tests

You need Python and git. Install pytest once, then run the tests from this folder:

```text
pip install pytest
pytest tests
```

A failing test names the document and the path or link to fix.

## Checks

Every pull request runs the organization's checks, which include the two tests. To run the rest of
the checks before each commit:

```text
pip install pre-commit
pre-commit install
```
