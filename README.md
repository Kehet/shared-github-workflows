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

## Available Workflows

### Auto Pull Request

Creates a pull request from one branch to another with an automatically generated changelog.

```yaml
jobs:
  auto-pr:
    uses: Kehet/shared-github-workflows/.github/workflows/auto-pull-request.yml@main
    # Optional parameters with their default values:
    with:
      source-branch: 'master'        # Source branch to create PR from
      target-branch: 'release-candidate'  # Target branch to create PR to
      pr-title-prefix: 'Release '    # Prefix for the PR title
      changelog-format: '* %s'       # Format for changelog entries
```

### Dependabot Auto Merge

Automatically merges Dependabot pull requests based on configurable update types.

```yaml
jobs:
  dependabot-merge:
    uses: Kehet/shared-github-workflows/.github/workflows/dependabot-auto-merge.yml@main
```

### Deployer Deployment

Deploys your application using deployphp and creates a GitHub release with an automatically generated changelog.

```yaml
jobs:
  deploy:
    uses: Kehet/shared-github-workflows/.github/workflows/deployphp-deployment.yml@main
    # Optional parameters with their default values:
    with:
      php-version: '8.3'              # PHP version to use
      source-branch: 'master'         # Source branch to deploy from
      target-branch: 'release-candidate'  # Target branch to update after deployment
      deployer-command: 'deploy'      # Deployer command to run
      changelog-format: '* %s'        # Format for changelog entries
      release-name-prefix: 'Release ' # Prefix for the release name
    secrets:
      private-key: ${{ secrets.PRIVATE_KEY }}  # Required: Private key for SSH connection
```

### Laravel Tests

Runs tests for Laravel applications with a MySQL database.

```yaml
jobs:
  tests:
    uses: Kehet/shared-github-workflows/.github/workflows/laravel-tests.yml@main
    # Optional parameters with their default values:
    with:
      php-version: '8.3'              # PHP version to use
      php-extensions: 'dom, curl, libxml, mbstring, zip, pcntl, pdo, sqlite, pdo_mysql, bcmath, soap, intl, gd, exif, iconv'  # PHP extensions to install
      mysql-version: '8.0'            # MySQL version to use
      mysql-database: 'testing'       # MySQL database name
      mysql-user: 'testing'           # MySQL username
      mysql-password: 'password'      # MySQL password
      mysql-root-password: 'password' # MySQL root password
      env-file: '.env.ci'             # Environment file to copy
      composer-install-options: '-n --prefer-dist'  # Options for composer install command
      run-migrations: true            # Whether to run migrations
      test-command: 'php artisan test' # Command to run tests
```
