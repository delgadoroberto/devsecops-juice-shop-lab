# Trivy Security Scanner

## Overview

**Trivy** is an open-source security scanner developed by Aqua Security. It is designed to identify security risks across different stages of the software development lifecycle.

In this laboratory, Trivy is integrated into a GitHub Actions workflow to automatically scan the OWASP Juice Shop application during every push and pull request.

The goal is to demonstrate how automated security controls can be incorporated into a DevSecOps pipeline to detect vulnerabilities before software is deployed.

---

# What Trivy Can Scan

Trivy supports multiple scan targets, including:

- Container images
- Filesystems
- Git repositories
- Infrastructure as Code (IaC)
- Kubernetes clusters
- Virtual machine images
- Software Bill of Materials (SBOM)
- Secrets
- Configuration files

This laboratory focuses on:

- Docker image scanning
- Filesystem scanning
- Secret detection

---

# How Trivy Works

The workflow follows these steps:

```text
GitHub Push
      │
      ▼
GitHub Actions
      │
      ▼
Download Trivy
      │
      ▼
Download Vulnerability Database
      │
      ▼
Scan Container Image
      │
      ▼
Scan Repository Files
      │
      ▼
Detect Secrets
      │
      ▼
Generate Security Report
```

---

# Vulnerability Severity

Trivy classifies findings using standard severity levels.

| Severity | Description |
|----------|-------------|
| UNKNOWN | Unknown impact |
| LOW | Low security risk |
| MEDIUM | Moderate security risk |
| HIGH | High security risk requiring remediation |
| CRITICAL | Severe vulnerability requiring immediate action |

This laboratory is configured to fail the pipeline when HIGH or CRITICAL vulnerabilities are detected.

---

# Security Checks Performed

The pipeline currently executes three security controls.

## Container Image Scan

Purpose:

- Detect vulnerable operating system packages.
- Detect vulnerable application dependencies.
- Identify outdated software.

Example:

```text
trivy image bkimminich/juice-shop
```

---

## Filesystem Scan

Purpose:

- Analyze project files.
- Detect vulnerable dependencies.
- Review application packages.

Example:

```text
trivy fs .
```

---

## Secret Detection

Purpose:

Detect accidentally exposed secrets such as:

- AWS keys
- Azure credentials
- Google Cloud credentials
- GitHub Personal Access Tokens
- SSH keys
- RSA private keys
- API keys

Example:

```text
trivy fs --scanners secret .
```

---

# Understanding the Results

A typical Trivy report contains:

- Package name
- Vulnerability identifier (CVE)
- Installed version
- Fixed version
- Severity
- Description

Example:

```text
Package: ws

CVE:
CVE-2024-37890

Installed:
7.4.6

Fixed:
8.17.1

Severity:
HIGH
```

This information helps determine:

- Which component is affected.
- The severity of the issue.
- Whether an update is available.

---

# Secret Detection Example

During execution, Trivy detected embedded RSA private keys within the OWASP Juice Shop source code.

Example:

```text
HIGH: AsymmetricPrivateKey

Location:

/juice-shop/lib/insecurity.ts
```

This behavior is expected because OWASP Juice Shop is intentionally vulnerable for educational purposes.

---

# Why the Pipeline Fails

The GitHub Actions workflow is configured with:

```yaml
exit-code: "1"
```

When HIGH or CRITICAL findings are detected, Trivy returns a non-zero exit code.

As a result, GitHub Actions marks the workflow as failed.

In a real-world DevSecOps environment, this prevents vulnerable software from progressing further in the CI/CD pipeline.

---

# Best Practices

When using Trivy in production environments:

- Scan every pull request.
- Scan every container image before publishing.
- Scan Infrastructure as Code templates.
- Detect secrets before deployment.
- Keep the vulnerability database updated.
- Generate SARIF reports for GitHub Security.
- Integrate with Dependency Review and CodeQL.

---

# References

- Trivy Documentation
- Aqua Security
- OWASP Juice Shop
- GitHub Actions
