# Workflows

A collection of github workflows for reuse. Some of the workflow files assume that files will exist in the original directory and will fail if they do not exist.

## `lint_python.yml`

### Inputs

- `python-version`: default 3.9

### Outputs

None

### Assumptions

- `requirements.txt` file at root level; specify packages needed by code to be linted
- `requirements-lint.txt` file at root level; specify versions of pylint and pyright for linting

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
