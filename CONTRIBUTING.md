# Contributing to ShieldCI

Thank you for your interest in contributing to ShieldCI! This document provides guidelines and instructions for contributing to the project.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [Project Structure](#project-structure)
- [Making Changes](#making-changes)
- [Testing](#testing)
- [Code Quality](#code-quality)
- [Submitting Changes](#submitting-changes)
- [Coding Standards](#coding-standards)
- [Documentation](#documentation)
- [Creating New Analyzers](#creating-new-analyzers)

## Code of Conduct

By participating in this project, you agree to maintain a respectful and inclusive environment for all contributors.

## Getting Started

1. **Fork the repository** on GitHub
2. **Clone your fork** locally:
   ```bash
   git clone https://github.com/YOUR_USERNAME/shieldci.git
   cd shieldci
   ```
3. **Add the upstream repository**:
   ```bash
   git remote add upstream https://github.com/shieldci/shieldci.git
   ```

## Development Setup

### Prerequisites

- PHP 8.1 or higher
- Composer 2.x
- Node.js 18+ (for example-app frontend)
- Git

### Install Dependencies

```bash
# Install analyzers-core dependencies
cd analyzers-core
composer install

# Install laravel package dependencies
cd ../laravel
composer install

# Install example-app dependencies
cd ../example-app
composer install
npm install
cp .env.example .env
php artisan key:generate
```

## Project Structure

```
shieldCI/
├── analyzers-core/      # Core analyzer engine (PHP 8.1+)
├── laravel/             # Laravel package
├── example-app/         # Demo Laravel application
├── docs/                # Documentation
├── strategy/            # Strategy and planning documents
└── .github/             # GitHub workflows and templates
```

### Key Directories

- **`analyzers-core/src/`**: Core abstracts, contracts, and utilities
- **`laravel/src/Analyzers/`**: All analyzer implementations
  - `Security/` - Security analyzers
  - `Performance/` - Performance analyzers
  - `Reliability/` - Reliability analyzers
  - `CodeQuality/` - Code quality analyzers
  - `BestPractices/` - Best practices analyzers
- **`laravel/src/Commands/`**: Artisan commands
- **`laravel/config/`**: Configuration files
- **`docs/docs/analyzers/`**: Analyzer documentation

## Making Changes

### 1. Create a Feature Branch

```bash
git checkout -b feature/my-new-feature
```

Branch naming conventions:
- `feature/` - New features
- `fix/` - Bug fixes
- `docs/` - Documentation updates
- `refactor/` - Code refactoring
- `perf/` - Performance improvements
- `test/` - Test updates

### 2. Make Your Changes

- Follow the [Coding Standards](#coding-standards)
- Write tests for new functionality
- Update documentation as needed
- Keep commits focused and atomic

### 3. Commit Your Changes

Use clear, descriptive commit messages:

```bash
git commit -m "feat: add SQL injection detection for raw queries"
```

Commit message format:
```
<type>: <subject>

<body (optional)>

<footer (optional)>
```

Types:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting)
- `refactor`: Code refactoring
- `perf`: Performance improvements
- `test`: Test updates
- `chore`: Build/tooling changes

## Testing

### Run Tests

```bash
# Analyzers Core
cd analyzers-core
composer test

# Laravel Package
cd laravel
composer test

# Example App
cd example-app
php artisan test
```

### Run Specific Tests

```bash
# Run specific test file
vendor/bin/phpunit tests/Unit/Analyzers/Security/AppKeyAnalyzerTest.php

# Run specific test method
vendor/bin/phpunit --filter testDetectsEmptyAppKey
```

### Test Coverage

```bash
# Generate coverage report
composer test-coverage

# Open coverage report
open coverage/index.html
```

### Writing Tests

- Place tests in the appropriate directory (`tests/Unit/` or `tests/Feature/`)
- Follow the naming convention: `*Test.php`
- Use descriptive test method names: `testDetectsEmptyAppKey`
- Include both positive and negative test cases
- Mock external dependencies

Example test structure:

```php
<?php

namespace ShieldCI\Tests\Unit\Analyzers\Security;

use ShieldCI\Tests\AnalyzerTestCase;

class MyAnalyzerTest extends AnalyzerTestCase
{
    public function testDetectsIssue(): void
    {
        // Arrange
        $this->setupTestFiles([
            'config/app.php' => '<?php return ["debug" => true];',
        ]);

        // Act
        $result = $this->runAnalyzer(MyAnalyzer::class);

        // Assert
        $this->assertFailed($result);
        $this->assertIssueCount(1, $result);
    }
}
```

## Code Quality

### Static Analysis

```bash
# Run PHPStan
composer analyse
```

### Code Formatting

```bash
# Analyzers Core (PHP-CS-Fixer)
cd analyzers-core
composer format

# Laravel Package (Pint)
cd laravel
composer format
```

### Check Formatting

```bash
# Check without making changes
composer format -- --dry-run --diff  # analyzers-core
composer format -- --test             # laravel
```

## Submitting Changes

### 1. Update Your Branch

```bash
git fetch upstream
git rebase upstream/master
```

### 2. Push to Your Fork

```bash
git push origin feature/my-new-feature
```

### 3. Create a Pull Request

1. Go to your fork on GitHub
2. Click "New Pull Request"
3. Select your feature branch
4. Fill out the PR template completely
5. Link related issues
6. Wait for CI checks to pass

### Pull Request Checklist

- [ ] Tests pass locally
- [ ] Code follows project standards
- [ ] Documentation updated
- [ ] Commit messages are clear
- [ ] PR description is complete
- [ ] Related issues are linked

## Coding Standards

### PHP Standards

- Follow **PSR-12** coding style
- Use **PHP 8.1+** features appropriately
- Use **strict types**: `declare(strict_types=1);`
- Use **type hints** for all parameters and return types
- Use **property types** for class properties

### Code Organization

- Keep methods small and focused (< 50 lines)
- Use early returns to reduce nesting
- Extract complex logic into private methods
- Use meaningful variable and method names
- Add PHPDoc blocks for complex methods

### Example

```php
<?php

declare(strict_types=1);

namespace ShieldCI\Analyzers\Security;

use ShieldCI\AnalyzersCore\Abstracts\AbstractFileAnalyzer;
use ShieldCI\AnalyzersCore\Contracts\ResultInterface;

final class MySecurityAnalyzer extends AbstractFileAnalyzer
{
    public function analyze(): ResultInterface
    {
        $issues = [];

        $this->checkConfiguration($issues);
        $this->checkImplementation($issues);

        return $this->formatResult($issues);
    }

    private function checkConfiguration(array &$issues): void
    {
        // Implementation
    }

    private function checkImplementation(array &$issues): void
    {
        // Implementation
    }
}
```

## Documentation

### Updating Documentation

When adding or modifying analyzers:

1. **Update analyzer documentation** in `docs/docs/analyzers/{category}/`
2. **Follow the documentation template**:

```markdown
---
title: Analyzer Name
description: Brief description
category: security
severity: high
tags: [tag1, tag2]
---

# Analyzer Name

Brief description of what the analyzer checks.

## What It Checks

Detailed explanation of the checks performed.

## Why It Matters

Explanation of the security/performance/reliability implications.

## How to Fix

### Quick Fix

Step-by-step instructions for fixing the issue.

### Example

**❌ Bad:**
```php
// Bad code example
```

**✅ Good:**
```php
// Good code example
```

## Configuration

Configuration options for this analyzer.

## References

- [Link to documentation]
- [Link to security advisory]
```

3. **Update the index file** if adding a new analyzer
4. **Update README** if adding major features

## Creating New Analyzers

### 1. Choose the Right Category

- **Security**: Vulnerabilities, security misconfigurations
- **Performance**: Performance bottlenecks, optimization opportunities
- **Reliability**: Error handling, stability issues
- **Code Quality**: Code smells, maintainability issues
- **Best Practices**: Laravel conventions, industry standards

### 2. Create the Analyzer Class

```bash
# Create the file
touch laravel/src/Analyzers/Security/MySecurityAnalyzer.php
```

### 3. Implement the Analyzer

```php
<?php

declare(strict_types=1);

namespace ShieldCI\Analyzers\Security;

use ShieldCI\AnalyzersCore\Abstracts\AbstractFileAnalyzer;
use ShieldCI\AnalyzersCore\Contracts\ResultInterface;
use ShieldCI\AnalyzersCore\Enums\Category;
use ShieldCI\AnalyzersCore\Enums\Severity;
use ShieldCI\AnalyzersCore\ValueObjects\AnalyzerMetadata;

final class MySecurityAnalyzer extends AbstractFileAnalyzer
{
    public function getMetadata(): AnalyzerMetadata
    {
        return new AnalyzerMetadata(
            id: 'my-security-check',
            name: 'My Security Analyzer',
            description: 'Checks for security issue X',
            category: Category::Security,
            severity: Severity::High,
            tags: ['security', 'configuration'],
            docsUrl: 'https://docs.shieldci.com/analyzers/security/my-security-check',
            timeToFix: 5
        );
    }

    public function shouldRun(): bool
    {
        // Return true if the analyzer should run
        return file_exists($this->buildPath('config', 'app.php'));
    }

    public function analyze(): ResultInterface
    {
        $issues = [];

        // Perform your checks
        $this->checkForIssue($issues);

        return empty($issues)
            ? $this->pass('No issues found')
            : $this->fail('Found security issues', $issues);
    }

    private function checkForIssue(array &$issues): void
    {
        // Implementation
    }
}
```

### 4. Create Tests

```bash
touch laravel/tests/Unit/Analyzers/Security/MySecurityAnalyzerTest.php
```

### 5. Create Documentation

```bash
touch docs/docs/analyzers/security/my-security-check.md
```

### 6. Register the Analyzer

The analyzer is automatically discovered via the service provider.

## Getting Help

- **Documentation**: Check the [docs](../docs/README.md)
- **Issues**: Search [existing issues](https://github.com/shieldci/shieldci/issues)
- **Discussions**: Join [GitHub Discussions](https://github.com/shieldci/shieldci/discussions)
- **Email**: support@shieldci.com

## License

By contributing to ShieldCI, you agree that your contributions will be licensed under the MIT License.

---

Thank you for contributing to ShieldCI! 🛡️

