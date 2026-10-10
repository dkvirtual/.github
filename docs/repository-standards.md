# Repository standards

## Purpose and documentation

Every repository has a clear purpose, a current README, an appropriate
`CODEOWNERS` file, and an intentional visibility setting.

Private, proprietary repositories do not need a `LICENSE` file or licensing
declaration to meet these standards. Do not add an open-source license by default.
For approved open-source publication or external distribution, specify the terms
for that release. Preserve applicable third-party licenses and notices.

The README explains setup, supported tool versions, example configuration, main
entry points, checks, and release usage. `AGENTS.md` supplies concise commands and
repository-specific constraints for coding agents. It must agree with the README
and actual tooling. Link to shared guidance instead of duplicating it.

Public documentation serves contributors and users. Use synthetic examples and
keep internal organization, access, and operational information private. Review
what is being disclosed, including examples, screenshots, and Git history;
automated secret scans cannot replace that judgment.

## Main branch and imports

`main` represents completed, usable work. Use issues and branches for unfinished
ideas and experiments, with visibility appropriate to their content. Remove
obsolete scaffolding, abandoned configuration, generated reports, session notes,
and commented-out experiments. Preserve useful tests, migrations, decisions, and
documentation that explain the current project.

Before importing code, verify its provenance and applicable third-party license
terms. Review files and history for secrets and information unsuitable for the
destination repository's audience. Resolve
findings and rotate any exposed credentials before publishing. Preserve useful,
publishable history; never silently rewrite a shared source repository's history.

## Changes and dependencies

Changes go through focused pull requests with meaningful checks. Use signed
commits and resolve review conversations. Follow the repository's configured
review and branch protections; these documents do not enforce GitHub settings.

Use reproducible tool versions and lockfiles. Dependabot is the standard dependency
updater. Review new dependencies, install scripts, permission changes, and release
provenance. See [Automation](automation.md) for shared workflow behavior.

## Verification and releases

Document a reliable command or small set of commands for local verification.
Test important behavior, failure cases, and compatibility. A green structural
check does not replace application tests or a human content review.

Identify releases by their source commit and immutable artifacts where applicable.
Include provenance and an SBOM for distributed application artifacts. Document
supported versions and user-facing breaking changes. Keep credentials out of
source files, build output, and pull request jobs.
