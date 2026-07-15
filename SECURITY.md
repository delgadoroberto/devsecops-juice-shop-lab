# Security Policy

## Overview

Security is the primary focus of this repository.

This laboratory demonstrates how automated security controls can be integrated into a Continuous Integration (CI) pipeline using GitHub Actions and Trivy. The project intentionally contains vulnerable components and example secrets for educational purposes.

Please read this policy before reporting security issues.

---

## Supported Versions

This repository is intended as an educational laboratory rather than production software.

Only the latest version available in the `main` branch is actively maintained.

| Version | Supported |
|----------|-----------|
| main | ✅ |
| Older commits | ❌ |

---

## Reporting a Vulnerability

If you discover an unintended security issue within the repository itself (excluding the intentionally vulnerable examples), please open a GitHub Issue describing:

- A clear description of the vulnerability
- Steps to reproduce
- Potential impact
- Suggested remediation (if available)

Please avoid publishing sensitive information directly in the issue description.

---

## Intentionally Vulnerable Content

This repository intentionally includes insecure examples for educational purposes.

Examples include:

- Hardcoded credentials
- Vulnerable container images
- Security misconfigurations

These examples exist solely to demonstrate how automated security tools detect common security weaknesses.

They must **not** be copied into production environments.

---

## Secret Management

Real credentials should never be committed to version control.

Instead, use secure secret management solutions such as:

- GitHub Secrets
- Azure Key Vault
- AWS Secrets Manager
- HashiCorp Vault

The `secrets.txt` file included in this repository contains sample credentials exclusively for demonstration purposes.

---

## Responsible Usage

This laboratory is designed for defensive security education.

It should only be deployed in controlled environments for learning, testing, or research.

Do not use this repository to target systems without explicit authorization.

---

## Security Scanning

The GitHub Actions workflow automatically performs several security checks, including:

- Container image vulnerability scanning
- Filesystem scanning
- Secret detection

Future versions of this laboratory may include additional controls such as:

- CodeQL
- Semgrep
- Hadolint
- SBOM generation
- Dependency review

---

## Remediation Guidance

If security findings are detected, recommended actions include:

- Remove exposed secrets
- Rotate compromised credentials
- Update vulnerable dependencies
- Upgrade container images
- Apply the principle of least privilege
- Re-run the CI pipeline after remediation

---

## Disclaimer

OWASP Juice Shop is intentionally vulnerable and is used exclusively as a learning platform.

The vulnerabilities demonstrated by this project are intentional and should never be considered acceptable in production environments.

Likewise, all credentials included in this repository are fictitious and exist solely to demonstrate automated secret detection.

---

## License

This repository is distributed under the MIT License.
