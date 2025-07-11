# Shared GitHub Workflows

A collection of reusable GitHub Actions workflows that can be shared across multiple repositories.

## Usage

To use these shared workflows in your repository, reference them in your workflow files using the `uses` keyword with the workflow path:

```yaml
name: Example Workflow

on:
  push:
    branches: [ main ]

jobs:
  example-job:
    uses: Kehet/shared-github-workflows/.github/workflows/example-workflow.yml@main
```

For workflows that require inputs, you can pass them as follows:

```yaml
jobs:
  example-job-with-inputs:
    uses: Kehet/shared-github-workflows/.github/workflows/example-workflow-with-inputs.yml@main
    with:
      php-version: '8.3'
    secrets:
      private-key: ${{ secrets.PRIVATE_KEY }}
```
