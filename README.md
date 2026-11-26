# Developer Guidelines

The source of truth for my development and AI-agent collaboration guidelines,
independent of technology stack.

## Repository contents

- [Shared guidelines](AI_GUIDELINESS_BASE.md).
- [Project guidelines template](templates/AI_GUIDELINESS.md).
- [Codex entry point](templates/AGENTS.md).
- [Claude entry point](templates/CLAUDE.md).
- [GitHub Copilot entry point](templates/copilot-instructions.md).
- [Pull request template](templates/pull_request_template.md).

## Adopting these guidelines in a project

1. Copy `templates/AI_GUIDELINESS.md` to the project root.
2. Record this repository, a full commit SHA, and how to access that exact
   revision. Replace the placeholders.
3. Document the actual stack, architecture, commands, and project-specific
   adaptations.
4. Copy each agent entry point to its supported location in the project, such as
   `AGENTS.md`, `CLAUDE.md`, or `.github/copilot-instructions.md`.
5. Copy and adapt the pull request template to `.github/pull_request_template.md`.
6. Before work begins, verify that the agent can read the pinned revision of the
   shared guidelines.

The reading order is: agent entry point → project guidelines → shared guidelines.
Each project pins a revision so updates are explicit. General rules do not need
to be copied into every project-specific guide.

## Maintenance

Update general rules here and project-specific decisions in the relevant project.
Use pull requests targeting `develop`, then stabilize and publish to `main` as
described in the shared guidelines. Initial repository creation is the bootstrap
exception; use the pull request workflow thereafter. This documentation repository
does not deploy a product.

## License

Released under the [MIT License](LICENSE).
