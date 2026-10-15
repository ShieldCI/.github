## ShieldCI

**Automated security, performance, and code-quality analysis for Laravel applications.**

ShieldCI scans your Laravel codebase and configuration for vulnerabilities, misconfigurations, and performance pitfalls, then tells you exactly how to fix them. Run it locally, gate merges in CI, or track results over time on [shieldci.com](https://shieldci.com).

```bash
composer require shieldci/laravel
php artisan shield:analyze
```

### Open-source packages

| Package | What it is |
|---|---|
| [**shieldci/laravel**](https://github.com/ShieldCI/laravel) | 70+ analyzers covering security, performance, reliability, code quality, and best practices. PHP 8.1+, Laravel 9–13. |
| [**shieldci/analyzers-core**](https://github.com/ShieldCI/analyzers-core) | A framework-agnostic foundation for building static analysis tools: analyzer base classes, AST parsing, and result formatters. |
| [**ShieldCI/docs**](https://github.com/ShieldCI/docs) | The source of [docs.shieldci.com](https://docs.shieldci.com), with a reference page for every analyzer. |

### Links

- 📚 [Documentation](https://docs.shieldci.com)
- 🛡️ [ShieldCI platform](https://shieldci.com)
- 🤝 [Contributing guide](https://github.com/ShieldCI/.github/blob/main/CONTRIBUTING.md)
- 🔒 [Security policy](https://github.com/ShieldCI/.github/blob/main/SECURITY.md). Please report vulnerabilities privately, never in public issues.
