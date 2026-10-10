# Repository readiness checklist

Use this checklist when preparing a new or imported repository for contributors.
Record only audience-appropriate evidence in its review. Mark an item **N/A with
a reason** when it does not apply.

## Content and publication

- [ ] Purpose, ownership, provenance, and repository visibility are clear.
- [ ] Applicable third-party licenses and notices are preserved. Project licensing
      terms are specified for open-source publication or external distribution;
      private, proprietary repositories do not require a `LICENSE` file or declaration.
- [ ] `main` contains completed work; unfinished work is tracked separately with
      appropriate visibility.
- [ ] Obsolete scaffolding and generated noise are removed; useful, publishable
      history, tests, migrations, and project documentation are preserved.
- [ ] Files and history have been manually reviewed for their intended audience,
      including examples, screenshots, internal planning, and access information.
- [ ] Files and history have been scanned for secrets; findings are resolved and
      exposed credentials revoked or rotated.
- [ ] README and `AGENTS.md` accurately describe setup, checks, and entry points.
- [ ] Local `CODEOWNERS`, editor settings, ignore rules, and synthetic example
      configuration are appropriate.

## Checks and dependencies

- [ ] A clean checkout can run documented checks with pinned tools and lockfiles.
- [ ] Relevant behavior and failure cases have meaningful tests.
- [ ] Configured branch protections and required checks match the contribution process.
- [ ] Shared workflows are explicitly adopted and pinned to reviewed commits.
- [ ] Actions are SHA-pinned, permissions are minimal, and untrusted PRs cannot
      access credentials or trigger privileged execution.
- [ ] Dependabot covers supported ecosystems; other dependency pins have a
      documented update process.
- [ ] Security findings have been reviewed and addressed before publication;
      sensitive evidence stays private.
- [ ] Community templates, support links, and private vulnerability reporting work.

## Releases, where applicable

- [ ] Releases identify the tested source commit and immutable artifacts.
- [ ] Distributed application artifacts have provenance and an SBOM.
- [ ] Supported versions, compatibility requirements, and breaking changes are documented.

## Automated coverage

`repository-baseline.yml` verifies the presence of `README.md`, `AGENTS.md`,
`.editorconfig`, `.github/CODEOWNERS`, and `.github/dependabot.yml`, and rejects
tracked environment-secret files and Terraform state/plan filenames. The secret
workflow separately scans Git history. Neither workflow determines whether other
information is appropriate to publish or certifies application security.
