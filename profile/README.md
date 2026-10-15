## ShieldCI

**Catch the security, performance, and reliability problems in your Laravel app — automatically, before they ship.**

ShieldCI is a Laravel-aware static analysis and security scanner. Its analyzers check your code and configuration for vulnerabilities, misconfigurations, and performance pitfalls, and every finding comes with a fix. It works alongside PHPStan and Larastan: they check your types, and ShieldCI checks security, performance, and reliability.

![ShieldCI scanning a Laravel app](https://raw.githubusercontent.com/ShieldCI/laravel/master/.github/assets/analyzer-terminal.gif)

```bash
composer require shieldci/laravel
php artisan shield:analyze
```

### Open source

| Package | What it is |
|---|---|
| [**shieldci/laravel**](https://github.com/ShieldCI/laravel) | 73 free, open-source analyzers for security, performance, reliability, code quality, and best practices. PHP 8.1+, Laravel 9+. |
| [**shieldci/analyzers-core**](https://github.com/ShieldCI/analyzers-core) | A framework-agnostic foundation for building PHP static analysis tools. |
| [**ShieldCI/docs**](https://github.com/ShieldCI/docs) | The source of [docs.shieldci.com](https://docs.shieldci.com): a detect-and-fix guide for every analyzer. |

### For teams

**ShieldCI Pro** adds 82 more analyzers (155 in total). On [shieldci.com](https://shieldci.com), your team gets a dashboard to track, assign, and resolve findings across every project and to gate merges in CI. **Start free.**

### Links

📚 [Documentation](https://docs.shieldci.com) · 🛡️ [shieldci.com](https://shieldci.com) · 🤝 [Contributing](https://github.com/ShieldCI/.github/blob/main/CONTRIBUTING.md) · 🔒 [Security policy](https://github.com/ShieldCI/.github/blob/main/SECURITY.md)
