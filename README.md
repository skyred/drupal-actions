# Drupal Github Actions
Once integrate with your Drupal project, this action will automatically run the list of jobs below (on commit):

- PHPUnit
- PHP Code Sniffer (PHPCS)
- PHPStan


## How to Use this GitHub Action

### Example Usage
1. Create a .github/workflows/drupal-ci.yml in the consuming repository:

```yaml
name: Drupal CI
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  drupal-ci:
    uses: your-org/drupal-ci-action@main
    with:
      drupal_version: '10.2'
      php_version: '8.3'
      mysql_version: '5.7'
      phpunit_coverage_path: 'coverage'
      phpunit_config_file: 'phpunit.xml'
      test_target_directory: 'modules/custom'
      junit_path: 'junit'
      simpletest_db: 'mysql://root:mysql_strong_password@mysql/drupal'
      browsertest_output_directory: '.tmp/browser_output'
      simpletest_base_url: 'http://localhost'
      phpcs_config_file: 'phpcs.xml'
      phpcs_target_directory: 'modules/custom themes/custom'
      phpstan_config_file: 'phpstan.neon'
```

### Prerequisites for Consuming Repositories

- composer.json:

```json
"require-dev": {
  "drupal/core-dev": "^10",
  "drupal/coder": "^8.3",
  "phpstan/phpstan": "^1.10"
}
```
- Run `composer install --dev` to install `phpunit/phpuni`t`, `drupal/coder` (for `phpcs`), and `phpstan/phpstan`.

- Configuration Files:

  - phpunit.xml: See [the documentation](https://www.drupal.org/docs/develop/automated-testing/phpunit-in-drupal/running-phpunit-tests#s-configure-phpunit) on Drupal.org
  - phpcs.xml: @todo
  - phpstan.neon @todo

### Inputs (Github Action parameters):

| Input | Description | Default | Required |
| ----- | ----------- | ------- | -------- |
| drupal_version | Drupal version for the container | latest | No |
| php_version | PHP version for the container | 8.4 | No |
| mysql_version | MySQL version for the service | latest | No |
| phpunit_coverage_path | Path for PHPUnit coverage output | coverage | No |
| phpunit_config_file | PHPUnit configuration file | phpunit.xml | No |
| test_target_directory | Target directory for tests | '' (empty) | No |
| junit_path | Path for JUnit output | junit | No |
| simpletest_db | Database connection string for Simpletest | mysql://root:mysql_strong_password@mysql/drupal | No |
| browsertest_output_directory | Browser test output directory | .tmp/browser_output | No |
| simpletest_base_url | Base URL for Simpletest | http://localhost | No |
| phpcs_config_file | PHPCS configuration file | phpcs.xml | No |
| phpcs_target_directory Target directory for PHPCS | modules/custom themes/custom | No |
| phpstan_config_file | PHPStan configuration file | phpstan.neon | No |