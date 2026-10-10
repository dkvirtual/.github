# Security policy

## Reporting a vulnerability

Do not open a public issue or pull request containing an unpatched vulnerability,
credential, personal information, or production data.

Use **Security → Report a vulnerability** on the affected repository when available.
For Deutsche Kraniche Virtual projects without that option, email
[security@dkvirtual.com](mailto:security@dkvirtual.com).

Include the affected repository and version, impact, a minimal reproduction, and
any suggested mitigation. Use synthetic data and redact credentials. Do not access
other users' data or disrupt a live service to demonstrate a finding.

## Supported versions and remediation

Each application states its supported releases in its own security policy. For
these shared workflows, fixes are maintained on `main`; consumers must update their
pinned workflow commit to receive them. No response-time guarantee is implied.

An exposed credential must be revoked or rotated. Removing it from the current
files or rewriting Git history alone is not sufficient remediation.
