# Security Policy

Thank you for helping keep ShieldCI and its users safe.

## Reporting a vulnerability

**Please do not report security issues through public GitHub issues, discussions, or pull requests.**

- **Open-source packages** (`shieldci/laravel`, `shieldci/analyzers-core`, and other public repositories in this organization): use GitHub's private vulnerability reporting. Click **Report a vulnerability** on the repository's **Security** tab.
- **shieldci.com and the ShieldCI platform**, or if you can't use GitHub: email **security@shieldci.com**.

Please include:

- the affected package version or URL/endpoint
- steps to reproduce, with a proof of concept where possible
- the impact you observed and what an attacker could achieve
- any logs, screenshots, or requests/responses that support the report

## What to expect

- We acknowledge reports within **3 business days**.
- We send an initial assessment within **10 business days** and keep you updated until the issue is resolved.
- When a fix ships, we publish a GitHub Security Advisory for affected packages and credit you unless you'd prefer to stay anonymous.

## Supported versions

Security fixes go into the latest minor release of each package. Please upgrade before reporting.

| Package | Supported |
|---|---|
| `shieldci/laravel` | latest `1.x` |
| `shieldci/analyzers-core` | latest `2.x` |
| shieldci.com | always current |

## Scope

In scope: the public packages in this organization, and shieldci.com including its subdomains and the authenticated application.

Generally out of scope, unless you show a concrete, exploitable impact:

- missing security headers, cookie flags, or best-practice configuration with no demonstrated attack
- SPF, DKIM, or DMARC configuration, and email spoofing
- clickjacking on pages with no sensitive actions
- version or banner disclosure, and verbose error pages without sensitive data
- rate limiting on non-sensitive endpoints
- reports produced only by automated scanners
- denial-of-service, volumetric, or social-engineering attacks
- vulnerabilities in third-party services we use, which should be reported to those vendors

## Safe harbor

We will not take legal action against research that:

- makes a good-faith effort to avoid privacy violations, data destruction, and service disruption
- only uses accounts you own or have explicit permission to test
- does not access, modify, or keep other users' data; if you encounter any, stop and tell us
- gives us reasonable time to fix the issue before any public disclosure

## Rewards

ShieldCI does not run a paid bug bounty program, and we do not offer payment in exchange for reports. We publicly credit valid findings in our security advisories.
