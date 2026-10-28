# Automation

## Reusable workflows

| Workflow | Interface | Behavior |
| --- | --- | --- |
| `.github/workflows/repository-baseline.yml` | `workflow_call`; optional `runner-labels` JSON array, no secrets | Checks the caller's local guidance/ownership files and tracked sensitive/generated filenames. |
| `.github/workflows/secret-scan.yml` | `workflow_call`; optional `runner-labels` JSON array, no secrets | Scans the caller's fetched Git history with checksum-verified Gitleaks. |

Both workflows default to GitHub-hosted `ubuntu-24.04` runners and use `contents: read`.
Trusted private callers may pass a JSON array through `with.runner-labels`.
Self-hosted callers must reject fork pull requests before scheduling jobs; the
shared workflows also reject fork PRs when a custom runner is selected.
This public repository retains GitHub-hosted checks, including external PRs.
Do not enable access to private self-hosted runners for public repositories.
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

## Job-local Node runtime

`.github/actions/setup-node` installs an exact, checksum-pinned Linux x64 Node
runtime in the job's temporary directory. It avoids runner-wide tool-cache writes,
which can mix ownership between container and native jobs. Pass `node-version` or
`node-version-file`; reviewed releases are 22.23.3, 24.21.0 and 24.22.1. For
Node 24 consumers, use 24.22.1 or a later reviewed security release; it includes
the [October 2026 security fixes](https://nodejs.org/en/blog/vulnerability/october-2026-security-releases).
Older pins remain for explicit consumer migration, not as a recommendation.
A version change must update its official SHA-256 here before consumers adopt it.

Private package callers may also set `registry-url: https://npm.pkg.github.com`
and `scope: '@dkvirtual'`; only their npm install/publish step receives
`NODE_AUTH_TOKEN`. The generated npm configuration contains an environment-variable
reference, never a credential. Pin this composite action to a reviewed commit.
