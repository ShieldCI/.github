# ShieldCI/.github

Default community health files for every public repository in the [ShieldCI organization](https://github.com/ShieldCI).

A repository uses these files automatically unless it has its own copy of the same file.

| File | Purpose |
|---|---|
| [`SECURITY.md`](SECURITY.md) | How to report vulnerabilities privately, scope, and safe harbor |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Development setup, quality checks, and pull request conventions |
| [`PULL_REQUEST_TEMPLATE.md`](PULL_REQUEST_TEMPLATE.md) | Default pull request description |
| [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE) | Bug report and feature request forms, plus contact links (security, docs, discussions) |
| [`profile/README.md`](profile/README.md) | The organization profile shown on [github.com/ShieldCI](https://github.com/ShieldCI) |

## Notes for maintainers

- Issue templates must stay in `.github/ISSUE_TEMPLATE/`. GitHub ignores an `ISSUE_TEMPLATE/` folder at the repository root.
- If a repository adds any file to its own `.github/ISSUE_TEMPLATE/`, it stops inheriting **all** of the default issue templates and contact links. Copy `config.yml` across if you do this.
- This repository must stay public. GitHub only applies these defaults from a public `.github` repository.

🔒 Found a vulnerability? See the [security policy](SECURITY.md). Please don't open a public issue.
