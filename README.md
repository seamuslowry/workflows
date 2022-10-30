# Workflows

A collection of github workflows for reuse. Some of the workflow files assume that files will exist in the original directory and will fail if they do not exist.

## `lint_python.yml`

### Inputs

- `python-version`: default 3.9; the version of python to use

### Secrets

None

### Outputs

None

### Assumptions

- `requirements.txt` file at root level; specify packages needed by code to be linted
- `requirements-lint.txt` file at root level; specify versions of pylint and pyright for linting. Example:

```
pylint==2.15.4
pyright==1.1.276
```

### Example

```yaml
jobs:
  lint:
    uses: seamuslowry/workflows/.github/workflows/lint_python.yml@main
```

## `publish_python.yml`

### Inputs

- `release-version`: required; the version to release
- `repo`: default `pypi`; what repo to publish the release to
- `python-version`: default 3.9; the version of python to use

### Secrets

- `py_pi_token`: required; the API token to use to publish

### Outputs

None

### Assumptions

- `requirements.txt` file at root level; specify packages needed by code to be linted
- `requirements-publish.txt` file at root level; specify versions of build and twine for publishing

```
build==0.8.0
twine==4.0.1
```

### Example

```yaml
jobs:
  publish:
    uses: seamuslowry/workflows/.github/workflows/publish_python.yml@main
    with:
      repo: testpypi
      release-version: 0.0.1
    secrets:
      py_pi_token: ${{ secrets.TEST_PYPI_API_TOKEN }}
```

## `test_python.yml`

### Inputs

- `min-coverage`: default 100; minimum percentage of code must be coverage
- `python-version`: default 3.9; the version of python to use

### Secrets

None

### Outputs

None

### Assumptions

- `requirements.txt` file at root level; specify packages needed by code to be linted
- `requirements-test.txt` file at root level; specify versions of pytest and coverage for testing and coverage

```
pytest==7.1.3
coverage==6.5.0
```

### Example

```yaml
jobs:
  test:
    uses: seamuslowry/workflows/.github/workflows/test_python.yml@main
```

## `tag.yml`

### Inputs

None

### Secrets

- `gh_token`: the GITHUB_TOKEN secret so it can create a tag

### Outputs

- `tag`: the semantic version string of the created tag

### Assumptions

None

### Example

```yaml
jobs:
  tag-new-version:
    uses: seamuslowry/workflows/.github/workflows/tag.yml@main
    secrets:
      gh_token: ${{ secrets.GITHUB_TOKEN }}
```
