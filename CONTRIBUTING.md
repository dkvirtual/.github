# Contributing

Use the repository's README and `AGENTS.md` for its purpose, setup, and verification
commands. If either is missing or inaccurate, include the correction in your change.

## Changes

1. Start from current `main`. Use a short branch such as `feat/export-report` or
   `fix/login-redirect`.
2. Keep each pull request focused on one outcome. Describe the problem, resulting
   behavior, and relevant compatibility considerations.
3. Run the repository's documented checks. Add tests for meaningful behavior and
   failure modes; documentation-only changes need appropriate documentation checks.
4. Open a pull request and resolve its checks and review conversations.

`main` must be usable and releasable. Track unfinished work in issues or branches,
not scratch files, stale implementation plans, or commented-out experiments.
Preserve useful tests, migration history, and project documentation.

Use signed commits and clear imperative commit messages. Prefer squash merges
with concise titles such as `fix: preserve the session after login`. Repository
rules determine which checks and reviews are enforced.

## Dependencies and sensitive changes

Commit lockfiles, pin runtime/tool versions, and use Dependabot for supported
dependency ecosystems. Explain new dependencies and review their maintenance,
permissions, and installation behavior.

Never commit credentials, production data, Terraform state, or real `.env` files.
Use example configuration with dummy values. Report vulnerabilities privately
under the [security policy](https://github.com/dkvirtual/.github/blob/main/SECURITY.md).

Explain permission changes and compatibility risks using non-sensitive examples.
Keep internal access conventions, operational details, and planning out of public
files, issues, and pull requests. Review imported history as well as current files
before publishing; secret scanning alone does not establish that content is public-safe.

Treat reviewers and contributors respectfully. Discuss the work, keep feedback
specific, and avoid sharing another person's private information.
