# 🚀 Quick Reference Guide

## 📋 Quick Commands

### Local Development

```bash
# Analyzers Core
cd analyzers-core
composer install          # Install dependencies
composer test            # Run tests
composer test-coverage   # Run tests with coverage
composer analyse         # Run PHPStan
composer format          # Format code

# Laravel Package
cd laravel
composer install          # Install dependencies
composer test            # Run tests
composer test-coverage   # Run tests with coverage
composer analyse         # Run PHPStan
composer format          # Format code (Pint)

# Example App
cd example-app
composer install          # Install PHP dependencies
npm install              # Install Node dependencies
cp .env.example .env     # Copy environment file
php artisan key:generate # Generate app key
php artisan test         # Run tests
php artisan shield:analyze # Run ShieldCI analysis
```

### Git Workflow

```bash
# Start new feature
git checkout -b feature/my-feature

# Make changes and commit
git add .
git commit -m "feat: add new feature"

# Update from master
git fetch upstream
git rebase upstream/master

# Push to your fork
git push origin feature/my-feature

# Create PR on GitHub
```

## 📝 Commit Message Format

```
<type>: <subject>

<body (optional)>

<footer (optional)>
```

**Types**:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `style`: Formatting
- `refactor`: Code refactoring
- `perf`: Performance
- `test`: Tests
- `chore`: Build/tools

**Examples**:
```bash
git commit -m "feat: add SQL injection analyzer"
git commit -m "fix: resolve false positive in AppKeyAnalyzer"
git commit -m "docs: update configuration guide"
```

## 🔍 Branch Naming

```
feature/   - New features
fix/       - Bug fixes
docs/      - Documentation
refactor/  - Code refactoring
perf/      - Performance
test/      - Tests
chore/     - Build/tools
```

**Examples**:
```bash
git checkout -b feature/add-xss-analyzer
git checkout -b fix/debug-mode-false-positive
git checkout -b docs/update-readme
```

## ✅ Pre-Push Checklist

- [ ] All tests pass locally
- [ ] Code formatted (`composer format`)
- [ ] PHPStan passes (`composer analyse`)
- [ ] Commit messages follow convention
- [ ] Branch is up to date with master
- [ ] No debug code or console logs

## 📊 Workflow Status Checks

### Required Checks (must pass)

- `analyzers-core / Analyzers Core Tests`
- `laravel-package / Laravel Package Tests` (all matrix)
- `example-app / Example App Tests`

### Optional Checks

- Code coverage reports
- Security scans

## 🎯 PR Submission

1. **Create PR** from your fork
2. **Fill template** completely
3. **Link issues** (Fixes #123)
4. **Wait for CI** to complete
5. **Address feedback** from reviewers
6. **Resolve conversations**
7. **Merge** when approved + green

## 🔒 Branch Protection Rules

### Master Branch

- ✅ Require PR before merge
- ✅ Require 1+ approvals
- ✅ Require status checks
- ✅ Require up-to-date branch
- ✅ Require conversation resolution
- ❌ No force pushes
- ❌ No deletions

## 📚 Documentation Files

| File | Purpose |
|------|---------|
| `SETUP_COMPLETE.md` | Setup summary |
| `WORKFLOWS_SETUP.md` | Detailed workflows |
| `BRANCH_PROTECTION.md` | Branch protection guide |
| `CONTRIBUTING.md` | Contribution guide |
| `QUICK_REFERENCE.md` | This file |

## 🧪 Testing Shortcuts

```bash
# Run specific test file
vendor/bin/phpunit tests/Unit/Analyzers/Security/AppKeyAnalyzerTest.php

# Run specific test method
vendor/bin/phpunit --filter testDetectsEmptyAppKey

# Run with coverage
vendor/bin/phpunit --coverage-html coverage

# Run only security analyzer tests
vendor/bin/phpunit tests/Unit/Analyzers/Security/
```

## 🎨 Code Style

### PHP Standards

- PSR-12 coding style
- Strict types: `declare(strict_types=1);`
- Type hints for all parameters
- Property types for all properties
- PHPDoc for complex methods

### File Structure

```php
<?php

declare(strict_types=1);

namespace ShieldCI\Analyzers\Security;

use ShieldCI\AnalyzersCore\Abstracts\AbstractFileAnalyzer;

final class MyAnalyzer extends AbstractFileAnalyzer
{
    public function analyze(): ResultInterface
    {
        // Implementation
    }
}
```

## 🔧 Troubleshooting

### Tests failing locally?

```bash
composer clear-cache
rm -rf vendor
composer install
composer test
```

### PHPStan errors?

```bash
composer analyse
# Fix reported issues
```

### Formatting issues?

```bash
composer format
git add .
git commit --amend --no-edit
```

### CI failing but local passes?

- Check PHP version matches
- Check Laravel version matches
- Test with `prefer-lowest` deps

## 📞 Getting Help

1. **Documentation**: Check `.github/` folder
2. **Issues**: Search existing issues
3. **Discussions**: GitHub Discussions
4. **Email**: support@shieldci.com

## 🎯 Common Tasks

### Add New Analyzer

1. Create analyzer class in `laravel/src/Analyzers/{Category}/`
2. Extend `AbstractFileAnalyzer`
3. Implement `analyze()` method
4. Create test in `tests/Unit/Analyzers/{Category}/`
5. Create docs in `docs/docs/analyzers/{category}/`
6. Update category index

### Fix Bug

1. Create test that reproduces bug
2. Fix the bug
3. Ensure test passes
4. Submit PR with "fix:" prefix

### Update Documentation

1. Edit relevant `.md` files
2. Check formatting
3. Submit PR with "docs:" prefix

### Add Test

1. Create test file in `tests/`
2. Follow naming convention
3. Use descriptive method names
4. Submit PR with "test:" prefix

## 🚀 Release Process

1. Update version in `composer.json`
2. Update `CHANGELOG.md`
3. Create release tag
4. Push tag to trigger release

## 📈 Metrics

### Coverage Targets

- Analyzers Core: >80%
- Laravel Package: >75%
- Overall: >75%

### Build Times

- Analyzers Core: ~2-3 min
- Laravel Package: ~15-20 min
- Example App: ~3-4 min

## 🎊 Quick Links

- [Actions](https://github.com/shieldci/shieldci/actions)
- [Issues](https://github.com/shieldci/shieldci/issues)
- [PRs](https://github.com/shieldci/shieldci/pulls)
- [Discussions](https://github.com/shieldci/shieldci/discussions)

---

**Keep this handy for quick reference! 📌**

