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

- `pip install '.[lint]'` will install all necessary dependencies for linting your project

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

- `pip install '.[publish]'` will install all necessary dependencies for publishing your project

### Example

```yaml
jobs:
  publish:
    uses: seamuslowry/workflows/.github/workflows/publish_python.yml@main
    with:
      repo: testpypi
      release-version: 0.0.1
      compose-file: docker-compose.yml
    secrets:
      py_pi_token: ${{ secrets.TEST_PYPI_API_TOKEN }}
```

## `test_python.yml`

### Inputs

- `min-coverage`: default 100; minimum percentage of code must be coverage
- `python-version`: default 3.9; the version of python to use
- `compose-file`: not required; expects a docker compose file; if passed, will build and up the file before tests and bring it down after

### Secrets

None

### Outputs

None

### Assumptions

- `pip install '.[test]'` will install all necessary dependencies for testing your project

### Example

```yaml
jobs:
  test:
    uses: seamuslowry/workflows/.github/workflows/test_python.yml@main
```

## `tag.yml`

### Inputs

- `with-v`: default false; whether to include v in tag version
- `dry-run`: default false; generate the next tag value but do not create the tag
- `custom-tag`: custom tag value to use; other tag related settings get ignored

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

## `deploy_python_functions.yml`

### Inputs

- `name`: the name of the functions app to deploy to
- `path`: default "."; the path to the project to deploy
- `python-version`: default 3.9; the version of python to use

### Secrets

- `azure_publish_profile`: the publish profile from azure to use; will include the deployment slot, if applicable

### Outputs

None

### Assumptions

None

### Example

```yaml
jobs:
  deploy:
    uses: seamuslowry/workflows/.github/workflows/deploy_python_functions.yml@main
    with:
      name: appname
    secrets:
      azure_publish_profile: ${{ secrets.AZURE_PROD_PUBLISH }}
```

## `lint_actions.yml`

### Inputs

- `reporter`: passthrough to [reporter](https://github.com/reviewdog/reviewdog#reporters) of [reviewdog](https://github.com/reviewdog/reviewdog). Use `github-pr-review` when run on PR actions and want to leave a review. Use `github-check` when running on push/merge and don't want a PR review.

### Secrets

- `gh_token`: the GITHUB_TOKEN secret so it can report

### Outputs

None

### Assumptions

None

### Example

```yaml
jobs:
  lint:
    uses: seamuslowry/workflows/.github/workflows/lint_actions.yml@main
    with:
      reporter: github-check
    secrets:
      gh_token: ${{ secrets.GITHUB_TOKEN }}
```
