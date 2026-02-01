# Branch Protection Configuration

This document describes how to configure branch protection rules for the ShieldCI repository to ensure code quality and prevent direct pushes to the master branch.

## GitHub Branch Protection Rules

To configure branch protection for the `master` (or `main`) branch:

1. Go to your repository on GitHub
2. Navigate to **Settings** → **Branches**
3. Click **Add branch protection rule**
4. Configure the following settings:

### Branch Name Pattern
```
master
```
(or `main` if that's your default branch)

### Protection Rules

#### ✅ Require a pull request before merging
- **Required approvals**: 1 (or more, depending on team size)
- ☑️ Dismiss stale pull request approvals when new commits are pushed
- ☑️ Require review from Code Owners (optional, if you have a CODEOWNERS file)

#### ✅ Require status checks to pass before merging
- ☑️ Require branches to be up to date before merging

**Required status checks** (select all that apply):
- `analyzers-core / Analyzers Core Tests`
- `laravel-package / Laravel Package Tests (8.1, 9.*)`
- `laravel-package / Laravel Package Tests (8.2, 9.*)`
- `laravel-package / Laravel Package Tests (8.2, 10.*)`
- `laravel-package / Laravel Package Tests (8.2, 11.*)`
- `laravel-package / Laravel Package Tests (8.3, 9.*)`
- `laravel-package / Laravel Package Tests (8.3, 10.*)`
- `laravel-package / Laravel Package Tests (8.3, 11.*)`
- `example-app / Example App Tests`

#### ✅ Require conversation resolution before merging
This ensures all review comments are addressed before merging.

#### ✅ Do not allow bypassing the above settings
Prevents administrators from bypassing these rules (recommended for production).

#### ❌ Allow force pushes
Keep this **disabled** to prevent force pushes to master.

#### ❌ Allow deletions
Keep this **disabled** to prevent accidental branch deletion.

## Workflow Files

The following GitHub Actions workflows have been configured:

### 1. Root Repository (`/.github/workflows/tests.yml`)
Runs tests for all packages in the monorepo:
- **analyzers-core**: Core analyzer engine tests
- **laravel-package**: Laravel package tests across multiple PHP and Laravel versions
- **example-app**: Example application tests and ShieldCI analysis

### 2. Analyzers Core (`/analyzers-core/.github/workflows/tests.yml`)
Standalone workflow for the analyzers-core package:
- Tests across PHP 8.1, 8.2, 8.3
- Both `prefer-lowest` and `prefer-stable` dependency versions
- PHPStan static analysis
- Code formatting checks
- Code coverage reporting

### 3. Laravel Package (`/laravel/.github/workflows/tests.yml`)
Standalone workflow for the Laravel package:
- Tests across PHP 8.1, 8.2, 8.3
- Tests across Laravel 9.x, 10.x, 11.x
- Both `prefer-lowest` and `prefer-stable` dependency versions
- PHPStan static analysis
- Code formatting checks (Laravel Pint)
- Code coverage reporting

### 4. Branch Protection (`/.github/workflows/branch-protection.yml`)
Ensures all required checks pass before allowing merge to master.

## Testing Locally Before Push

Before pushing your changes, run these commands locally:

### Analyzers Core
```bash
cd analyzers-core
composer install
composer test
composer analyse
composer format
```

### Laravel Package
```bash
cd laravel
composer install
composer test
composer analyse
composer format
```

### Example App
```bash
cd example-app
composer install
npm install
cp .env.example .env
php artisan key:generate
php artisan test
php artisan shield:analyze
```

## Continuous Integration Flow

1. **Developer creates a feature branch**
   ```bash
   git checkout -b feature/my-new-feature
   ```

2. **Developer makes changes and commits**
   ```bash
   git add .
   git commit -m "feat: add new feature"
   ```

3. **Developer pushes to GitHub**
   ```bash
   git push origin feature/my-new-feature
   ```

4. **Developer creates a Pull Request**
   - GitHub Actions automatically runs all tests
   - Code quality checks are performed
   - Coverage reports are generated

5. **Review Process**
   - At least 1 reviewer approves the PR
   - All status checks must pass (green ✅)
   - All conversations must be resolved

6. **Merge to Master**
   - Once approved and all checks pass, the PR can be merged
   - Direct pushes to master are blocked

## Troubleshooting

### Tests Failing in CI but Passing Locally

1. **Check PHP version**: Ensure you're testing with the same PHP version as CI
2. **Clear caches**: Run `composer clear-cache` and reinstall dependencies
3. **Check environment**: Ensure `.env` settings match CI expectations

### Status Checks Not Appearing

1. **First run**: Status checks only appear after the workflow runs at least once
2. **Workflow syntax**: Check for YAML syntax errors in workflow files
3. **Permissions**: Ensure GitHub Actions has permission to run workflows

### Bypass Protection (Emergency Only)

If you need to bypass protection rules in an emergency:
1. Go to **Settings** → **Branches**
2. Temporarily disable the rule
3. Make your changes
4. **Immediately re-enable the rule**

⚠️ **Note**: This should only be done in critical situations and should be documented.

## Additional Resources

- [GitHub Branch Protection Documentation](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [ShieldCI Documentation](../docs/README.md)

