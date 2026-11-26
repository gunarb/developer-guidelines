# Repository Guidelines

Read [AI_GUIDELINESS_BASE.md](AI_GUIDELINESS_BASE.md) in full. It is the local
source of truth for this repository and avoids relying on a remote copy to maintain
the shared guidelines themselves.

## Scope and validation

This repository contains Markdown guidelines and templates. Keep examples
technology-agnostic. Review consistency, local links, and `git diff --check`.
No build is required. Unfilled adoption references in templates are intentional.
Write and maintain this repository's documentation in English.

## Git

Follow the branching strategy in the shared guidelines. Initial repository
creation is the only bootstrap exception to the pull request requirement. GitHub
protects `main`: changes require a pull request, including for administrators;
force pushes and branch deletion are disabled. No approvals or status checks are
required. There is no automatic deployment or configured CI check.
