# GitHub Actions Permissions Update

## Overview
This document describes the permissions updates made to GitHub Actions workflows in this repository to follow security best practices and the principle of least privilege.

## Changes Made

### 1. CI Workflow (`.github/workflows/ci.yml`)
Added explicit workflow-level permissions:
- `contents: read` - Allows the workflow to check out repository code
- `actions: write` - Allows the workflow to upload artifacts
- `pull-requests: write` - Allows the workflow to interact with pull requests

**Rationale**: The CI workflow performs the following actions that require these permissions:
- Checks out code using `actions/checkout@v4`
- Uploads test artifacts using `actions/upload-artifact@v4`
- Runs on pull requests and may need to add comments or update status

### 2. CodeQL Workflow (`.github/workflows/codeql-analysis.yml`)
Added explicit workflow-level permissions:
- `actions: read` - Allows the workflow to access workflow run information
- `contents: read` - Allows the workflow to check out repository code
- `security-events: write` - Allows the workflow to upload security scanning results

**Rationale**: The CodeQL workflow performs security scanning and needs to:
- Check out code for analysis
- Upload security findings to GitHub Security tab
- Access workflow metadata

## Security Benefits

1. **Explicit Permissions**: By declaring permissions explicitly, we follow the principle of least privilege
2. **Auditability**: It's clear what each workflow can and cannot do
3. **GitHub Security Best Practices**: Aligns with GitHub's recommendations for secure workflows
4. **Defense in Depth**: Limits potential impact if a workflow is compromised

## Compatibility

These changes are backward compatible and do not affect the functionality of existing workflows. The permissions granted match what the workflows were already using implicitly.

## References

- [GitHub Actions: Permissions for the GITHUB_TOKEN](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#permissions-for-the-github_token)
- [GitHub Actions Security Best Practices](https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions)
