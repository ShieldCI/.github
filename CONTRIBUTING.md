# Contributing to ShieldCI

Thanks for your interest in contributing! These guidelines apply to every public repository in the [ShieldCI organization](https://github.com/ShieldCI).

> **Found a security issue?** Don't open an issue or pull request. Follow the [security policy](https://github.com/ShieldCI/.github/blob/main/SECURITY.md) instead.

## Before you start

- **Bugs and small fixes:** open a pull request directly, or open an issue first if you're unsure.
- **New analyzers or larger changes:** open an issue first so we can agree on the approach before you put in the work.
- Search existing issues to avoid duplicates.

## Development setup

1. Fork the repository you want to change and clone your fork.
2. Install dependencies with `composer install` (or `npm install` for `docs`).
3. Create a branch off `master`: `feature/…`, `fix/…`, `docs/…`, `refactor/…`, or `test/…`.

## Quality checks

Every PHP package runs the same checks in CI. Run them locally before pushing:

```bash
composer check      # formatting check + PHPStan (level 9) + tests
composer format     # apply the formatter (Pint or PHP-CS-Fixer, per repo)
```

Pull requests must:

- pass `composer check` with no new PHPStan errors
- include tests for new behavior and for every bug fix
- use `declare(strict_types=1);` and full parameter and return type hints
- update the relevant docs page when behavior changes (analyzer docs live in [ShieldCI/docs](https://github.com/ShieldCI/docs))

## Commits and pull requests

- Use [Conventional Commits](https://www.conventionalcommits.org/): `feat:`, `fix:`, `docs:`, `refactor:`, `perf:`, `test:`, `chore:`.
- Keep each pull request focused on one change, and fill in the pull request template.
- Link the issue it resolves (`Fixes #123`).

## License

By contributing, you agree that your contributions are licensed under the MIT License of the repository you're contributing to.
