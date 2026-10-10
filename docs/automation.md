# Automation

## Reusable workflows

| Workflow | Interface | Behavior |
| --- | --- | --- |
| `.github/workflows/repository-baseline.yml` | `workflow_call`; no inputs or secrets | Checks the caller's local guidance/ownership files and tracked sensitive/generated filenames. |
| `.github/workflows/secret-scan.yml` | `workflow_call`; no inputs or secrets | Scans the caller's fetched Git history with checksum-verified Gitleaks. |

Both workflows use GitHub-hosted `ubuntu-24.04` runners and `contents: read`.
They check out the caller's repository without retaining Git credentials and
report check results. They have no deployment or repository-administration role.

Each consumer must create its own workflow. The following is an adoption example:
replace `FULL_REVIEWED_COMMIT_SHA` with an actual 40-character commit from this
repository before use. Do not use a mutable branch or release tag instead.

```yaml
name: Repository checks
on:
  pull_request:
  push:
    branches: [main]
permissions:
  contents: read
jobs:
  baseline:
    uses: dkvirtual/.github/.github/workflows/repository-baseline.yml@FULL_REVIEWED_COMMIT_SHA
  secrets:
    uses: dkvirtual/.github/.github/workflows/secret-scan.yml@FULL_REVIEWED_COMMIT_SHA
```

The `.github` repository itself uses local workflow references, which resolve to
the same commit as its caller. After adoption, use the actual successful check names
shown by GitHub when configuring required status checks. These workflows do not
inherit or establish organization enforcement.

## Dependency updates

- Use Dependabot for supported dependencies; each repository declares its own
  ecosystems and update configuration.
- In this repository, routine Actions updates run monthly with a seven-day
  cooldown. All Actions version updates are grouped into one PR, with at most one
  version-update PR open at a time. Cooldown and this PR limit do not apply to
  security updates.
- Keep security alerts and security-update PRs enabled where supported.
- GitHub currently does not generate Dependabot alerts for SHA-pinned Actions
  ([documented limitation](https://docs.github.com/en/code-security/reference/supply-chain-security/dependency-graph-supported-package-ecosystems)).
  Review upstream security advisories and promptly propose fixes outside the
  monthly schedule when needed; do not rely on security-update PRs alone.
- This repository's workflows do not auto-merge or auto-approve PRs. Review code and
  permission changes; an update being a patch is not itself a trust signal.
- The standalone Gitleaks and actionlint version/checksum pins are reviewed manually
  at least monthly and promptly for relevant security advisories. Dependabot does
  not maintain these embedded binary pins. Update a version and its SHA-256 together,
  verify the upstream release, and exercise the check before merging.

## Supply chain and workflow boundaries

Pin external Actions to full commit SHAs, include a release comment for review,
and verify downloaded tools against a pinned digest before execution. A matching
checksum proves the download matches the reviewed artifact; it does not establish
that upstream code is safe.

Keep pull request workflows read-only. Never execute untrusted PR code through
`pull_request_target` or a privileged follow-up job. Do not pass all repository
secrets into shared workflows. Restrict deployment credentials to the required
repository, environment, and job. Prefer short-lived credentials where supported.

Use native secret scanning/push protection when available, alongside Gitleaks.
Findings require remediation; rotate leaked credentials rather than only suppressing
the scanner. Any scanner allowlist must identify its reason and reviewer.
