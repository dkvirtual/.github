# Repository and Git naming

Use **Deutsche Kraniche Virtual** as the organization name in prose. The GitHub
organization identifier is `dkvirtual` in repository references and URLs.

Use lowercase, descriptive, hyphen-separated repository names. Prefer an existing
name over renaming a repository solely for aesthetics.

| Resource | Convention | Example |
| --- | --- | --- |
| Repository | Describe its purpose; omit a redundant organization prefix | `example-library` |
| Default branch | `main` | `main` |
| Work branch | `feat/`, `fix/`, `docs/`, or `chore/`, followed by a short purpose | `fix/broken-link` |
| Release tag | Semantic version with a `v` prefix, when the project publishes releases | `v1.2.3` |

`.github` is GitHub's reserved name for this repository.
