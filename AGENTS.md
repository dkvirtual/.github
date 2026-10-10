# Working in this repository

This public repository contains contribution defaults and reusable GitHub Actions
for Deutsche Kraniche Virtual.
Keep it small, public-safe, and useful to both people and coding agents.

- Read `README.md` and the relevant document in `docs/` before editing.
- Keep accepted guidance in `main`; put proposals and unfinished work in issues or
  branches. Do not add session transcripts, scratch plans, or generated reports.
- Publish only contributor-facing guidance and documentation of this repository's
  tooling. Keep internal identity and access conventions, organization structure,
  infrastructure plans, inventories, and operational runbooks out of this repository.
- Do not add credentials, private account information, or application data. Use
  generic examples, and manually review both files and history for information
  that should not be public; passing a secret scan is not publication approval.
- Use **Deutsche Kraniche Virtual** in prose. Use `dkvirtual` only as the GitHub
  organization identifier in repository references and URLs.
- Do not change organization settings or other repositories as a side effect.
  A task must explicitly include those changes.
- Pin external Actions and reusable workflows to full commit SHAs. Pin downloaded
  executables to versions and verified checksums; never pipe downloads into a shell.
- Keep workflow permissions minimal. Do not execute untrusted pull request code in
  a privileged context, use `pull_request_target` for builds, or inherit all secrets.
- Preserve the distinction between GitHub-inherited defaults and files each
  repository must adopt explicitly.
- Shared workflows must work with the caller's checkout and require no secrets.
  Document compatibility changes before changing their interface or job names.
- Run `actionlint`, `gitleaks dir --redact --no-banner .`, and `git diff --check`.
  Also run `gitleaks git --redact --no-banner .` when history is available.
- Report what changed, which checks ran, and any checks that could not run.
