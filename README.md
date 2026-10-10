# Deutsche Kraniche Virtual

Shared contribution guidance, issue and pull request templates, and reusable
GitHub Actions workflows for Deutsche Kraniche Virtual repositories.

Start with [Contributing](CONTRIBUTING.md), the
[repository standards](docs/repository-standards.md), and the
[readiness checklist](docs/repo-readiness-checklist.md).

## What is shared

| Content | How a repository adopts it |
| --- | --- |
| `CONTRIBUTING.md`, `SECURITY.md`, `SUPPORT.md` | GitHub displays the defaults when the repository has no corresponding file. |
| Issue and pull request templates | GitHub supplies defaults when the repository has no overriding templates. |
| Reusable workflows | Each repository explicitly calls a reviewed commit of the workflow. |
| `AGENTS.md`, `CODEOWNERS`, Dependabot, editor settings | Each repository maintains its own files. These are not inherited. |
| Branch rules and organization settings | Configured separately in GitHub. Files in this repository do not enforce them. |

This public repository contains guidance for contributors and documentation for its
shared tooling. Internal organization and operational documentation belongs in
private repositories. Review content for its intended audience before publishing;
a secret scanner cannot determine whether information should be public.

Defaults do not appear in consumer clones, so each repository's README and
`AGENTS.md` must contain its essential local commands.

## Checks

The CI workflow runs:

- **Repository baseline:** required local guidance and ownership files, plus checks
  for sensitive environment and state filenames. This is a structural check, not
  a content review or security audit.
- **Secret scanning:** Gitleaks scans the fetched Git history with redacted output.
- **Workflow lint:** actionlint checks the workflow definitions and embedded scripts.

Checks run for pull requests, pushes to `main`, manual requests, and weekly.
Workflows use read-only repository permissions and do not receive deployment secrets.

For local checks, use Git, Python 3, actionlint **1.7.12**, and Gitleaks **8.30.1**:

```sh
actionlint
gitleaks dir --redact --no-banner .
gitleaks git --redact --no-banner .
git diff --check
```

The directory scan includes edits that have not been committed; the Git scan checks
history. CI pins its downloaded tools to reviewed SHA-256 checksums.

## Adoption and maintenance

See [Automation](docs/automation.md) for workflow adoption, dependency updates,
and the boundary between documentation and enforced policy. Use the
[naming convention](docs/naming.md) when adding repositories, branches, or release tags.

Report sensitive findings using the [security policy](SECURITY.md).

No open-source license is granted by this repository. These standards do not
require a `LICENSE` file or licensing declaration for private, proprietary
repositories. Specify project terms when publishing open source or distributing
externally, and preserve applicable third-party licenses and notices. GitHub does
not inherit licenses from `.github`.
