# GitHub Workflows Setup Summary

This document provides an overview of the GitHub Actions workflows and related files that have been configured for the ShieldCI project.

## 📋 Overview

The ShieldCI project now has comprehensive CI/CD workflows that automatically run tests, code quality checks, and coverage reports before allowing merges to the master branch.

## 🔧 Workflow Files Created

### 1. Root Repository Workflows

#### `.github/workflows/tests.yml`
**Purpose**: Main workflow for the monorepo that tests all packages

**Jobs**:
- `analyzers-core`: Tests the core analyzer engine
- `laravel-package`: Tests the Laravel package across multiple PHP and Laravel versions
  - PHP: 8.1, 8.2, 8.3
  - Laravel: 9.x, 10.x, 11.x
  - Matrix excludes Laravel 11 on PHP 8.1 (incompatible)
- `example-app`: Tests the example application and runs ShieldCI analysis

**Triggers**:
- Push to `master`, `main`, or `develop` branches
- Pull requests to `master`, `main`, or `develop` branches

**Features**:
- Dependency caching for faster builds
- Parallel test execution across matrix
- Uploads ShieldCI report as artifact
- Runs on every push and PR

#### `.github/workflows/branch-protection.yml`
**Purpose**: Ensures all required checks pass before merging

**Jobs**:
- `check-required-status`: Waits for all test jobs to complete successfully

**Triggers**:
- Pull requests to `master` or `main` branches

### 2. Analyzers Core Workflows

#### `analyzers-core/.github/workflows/tests.yml`
**Purpose**: Standalone workflow for the analyzers-core package

**Jobs**:
- `test`: Runs tests across PHP versions and dependency versions
  - PHP: 8.1, 8.2, 8.3
  - Dependencies: prefer-lowest, prefer-stable
  - OS: Ubuntu latest
- `code-quality`: Runs PHPStan and code formatting checks
- `coverage`: Generates code coverage and uploads to Codecov

**Triggers**:
- Push to `master`, `main`, or `develop` branches
- Pull requests to `master`, `main`, or `develop` branches

**Features**:
- Matrix testing across PHP versions
- Static analysis with PHPStan
- Code formatting validation with PHP-CS-Fixer
- Code coverage reporting

### 3. Laravel Package Workflows

#### `laravel/.github/workflows/tests.yml`
**Purpose**: Standalone workflow for the Laravel package

**Jobs**:
- `test`: Runs tests across PHP and Laravel versions
  - PHP: 8.1, 8.2, 8.3
  - Laravel: 9.x, 10.x, 11.x
  - Dependencies: prefer-lowest, prefer-stable
  - Matrix excludes incompatible combinations
- `code-quality`: Runs PHPStan and Pint formatting checks
- `coverage`: Generates code coverage and uploads to Codecov

**Triggers**:
- Push to `master`, `main`, or `develop` branches
- Pull requests to `master`, `main`, or `develop` branches

**Features**:
- Comprehensive matrix testing
- Dynamic Laravel version installation
- Static analysis with PHPStan
- Code formatting validation with Laravel Pint
- Code coverage reporting

## 📝 Template Files Created

### Issue Templates

#### `.github/ISSUE_TEMPLATE/bug_report.md`
**Purpose**: Standardized template for bug reports

**Sections**:
- Bug description
- Affected component
- Steps to reproduce
- Expected vs actual behavior
- Environment details
- Stack trace
- Screenshots

#### `.github/ISSUE_TEMPLATE/feature_request.md`
**Purpose**: Standardized template for feature requests

**Sections**:
- Feature description
- Problem statement
- Proposed solution
- Use cases and examples
- Implementation suggestions
- Impact assessment
- Priority level

#### `.github/ISSUE_TEMPLATE/config.yml`
**Purpose**: Configure issue template options

**Features**:
- Disables blank issues
- Provides links to documentation
- Links to discussions
- Security vulnerability reporting

### Pull Request Template

#### `.github/PULL_REQUEST_TEMPLATE.md`
**Purpose**: Comprehensive PR template

**Sections**:
- Description and type of change
- Related issues
- Changes made
- Affected modules
- Testing evidence
- Code quality checks
- Documentation updates
- Security considerations
- Performance impact
- Breaking changes
- Reviewer checklist

## 📚 Documentation Files Created

### `.github/BRANCH_PROTECTION.md`
**Purpose**: Guide for configuring branch protection rules

**Contents**:
- Step-by-step GitHub branch protection setup
- Required status checks list
- Workflow descriptions
- Local testing instructions
- CI/CD flow explanation
- Troubleshooting guide

### `.github/CONTRIBUTING.md`
**Purpose**: Comprehensive contribution guide

**Contents**:
- Getting started instructions
- Development setup
- Project structure overview
- Making changes workflow
- Testing guidelines
- Code quality standards
- Submitting changes process
- Coding standards
- Documentation guidelines
- Creating new analyzers guide

### `.github/CODEOWNERS`
**Purpose**: Automatic reviewer assignment

**Owners Defined**:
- `@shieldci/core-team` - Default owners
- `@shieldci/analyzers-team` - Analyzers core
- `@shieldci/laravel-team` - Laravel package
- `@shieldci/security-team` - Security analyzers
- `@shieldci/performance-team` - Performance analyzers
- `@shieldci/docs-team` - Documentation
- `@shieldci/devops-team` - Workflows
- `@shieldci/leadership-team` - Strategy docs

### Root `README.md`
**Purpose**: Main project README with badges and quick start

**Contents**:
- Project overview
- Feature highlights
- Repository structure
- Development status with badges
- Quick start guide
- Documentation links
- Development setup
- Contributing guidelines
- License and credits

## 🚀 How to Use

### For Contributors

1. **Fork and clone** the repository
2. **Create a feature branch**: `git checkout -b feature/my-feature`
3. **Make changes** following the coding standards
4. **Run tests locally**:
   ```bash
   cd analyzers-core && composer test
   cd ../laravel && composer test
   ```
5. **Push and create PR**: GitHub Actions will automatically run all checks
6. **Wait for approval**: All checks must pass before merge

### For Maintainers

1. **Configure branch protection** following `.github/BRANCH_PROTECTION.md`
2. **Set up teams** mentioned in `.github/CODEOWNERS`
3. **Configure Codecov** (optional) for coverage reports
4. **Review PRs** using the PR template checklist
5. **Merge** only when all checks pass

## 🔒 Branch Protection Configuration

To enable branch protection:

1. Go to **Settings** → **Branches** on GitHub
2. Add rule for `master` branch
3. Enable:
   - ✅ Require pull request reviews (1+ approvals)
   - ✅ Require status checks to pass
   - ✅ Require branches to be up to date
   - ✅ Require conversation resolution
   - ❌ Allow force pushes (disabled)
   - ❌ Allow deletions (disabled)

4. Select required status checks:
   - `analyzers-core / Analyzers Core Tests`
   - `laravel-package / Laravel Package Tests` (all matrix combinations)
   - `example-app / Example App Tests`

## 📊 Workflow Status

You can monitor workflow status:

- **Actions tab**: https://github.com/shieldci/shieldci/actions
- **README badges**: Show current build status
- **PR checks**: Visible on each pull request

## 🔧 Maintenance

### Updating Workflows

When updating workflows:

1. Edit the `.yml` files
2. Test locally using [act](https://github.com/nektos/act) (optional)
3. Commit and push to a feature branch
4. Create a PR to test the workflow changes
5. Merge once verified

### Adding New PHP/Laravel Versions

To add support for new versions:

1. Update the matrix in workflow files:
   ```yaml
   matrix:
     php: [8.1, 8.2, 8.3, 8.4]  # Add new version
     laravel: [9.*, 10.*, 11.*, 12.*]  # Add new version
   ```

2. Update exclusions if needed:
   ```yaml
   exclude:
     - laravel: 12.*
       php: 8.1  # If incompatible
   ```

3. Update `composer.json` requirements
4. Test thoroughly

## 📈 Coverage Reports

Code coverage is automatically generated and uploaded to Codecov:

- **Analyzers Core**: Runs on PHP 8.2
- **Laravel Package**: Runs on PHP 8.2
- **Reports**: Available in Codecov dashboard

To view coverage locally:
```bash
composer test-coverage
open coverage/index.html
```

## 🎯 Next Steps

1. **Configure GitHub repository settings**:
   - Enable branch protection
   - Set up required reviewers
   - Configure team permissions

2. **Set up Codecov** (optional):
   - Create Codecov account
   - Link repository
   - Configure coverage thresholds

3. **Create teams** mentioned in CODEOWNERS:
   - `@shieldci/core-team`
   - `@shieldci/analyzers-team`
   - `@shieldci/laravel-team`
   - `@shieldci/security-team`
   - `@shieldci/performance-team`
   - `@shieldci/docs-team`
   - `@shieldci/devops-team`
   - `@shieldci/leadership-team`

4. **Test the workflows**:
   - Create a test PR
   - Verify all checks run
   - Confirm branch protection works

## 🆘 Troubleshooting

### Workflows Not Running

- Check GitHub Actions is enabled in repository settings
- Verify workflow files are in `.github/workflows/`
- Check YAML syntax is valid

### Tests Failing in CI

- Compare PHP versions (local vs CI)
- Check dependency versions
- Review CI logs for specific errors
- Test with `prefer-lowest` dependencies locally

### Coverage Not Uploading

- Verify Codecov token is configured
- Check network access in workflow
- Review Codecov action logs

## 📞 Support

For questions or issues:

- **Documentation**: See `.github/CONTRIBUTING.md`
- **Issues**: Create an issue using the templates
- **Discussions**: Use GitHub Discussions
- **Email**: support@shieldci.com

---

**Last Updated**: December 2025
**Maintained By**: ShieldCI DevOps Team

