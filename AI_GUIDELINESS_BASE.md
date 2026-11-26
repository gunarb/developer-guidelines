# AI-Assisted Development Guidelines

The shared source of truth for starting and working on projects together. These
rules are independent of product, technology stack, infrastructure, and folder
structure. Apply each rule when relevant to the work.

## Scope and adaptation

- Read this document in full before analyzing or modifying a project.
- Record architecture, commands, product languages, and project-specific decisions
  in a separate project-guidelines document; do not mix them into this shared base.
- Explicit project adaptations take precedence over this base within their scope.
  Direct user instructions and higher-priority instructions always take precedence.
- Keep general rules here and avoid duplicating them in other documents.
- When reusing this base in another repository, review its existing instructions
  and resolve conflicts before implementing. Copies are not synchronized
  automatically across repositories.

## 1. Before implementation

- Read the repository instructions and check the Git status.
- Inspect relevant code, data, components, and documentation.
- Identify what to reuse, extend, or create. Preserve changes made by others.
- Keep changes focused; track unrelated improvements separately.
- Avoid unrelated refactors, renames, mass formatting, or dependencies.

## 2. Code clarity and design

- Keep the main flow easy to follow; prefer guard clauses when they reduce
  nesting. Do not split simple operations into empty abstractions.
- Name things for their domain meaning and responsibility. Booleans should
  express statements or questions, such as `isAvailable` or `canPublish`.
- Use the same term for the same concept across UI, contracts, and data.
- Separate composition, business rules, and side effects. Pages or routes
  coordinate; specific responsibilities belong in modules appropriate to the
  framework.
- Encapsulate external integrations behind clear boundaries when that improves
  isolation or testability. Do not add layers, interfaces, or classes without a
  concrete need.
- Validate inputs at trust boundaries and represent states with precise types;
  avoid contradictory boolean combinations and ambiguous values.
- Keep contracts explicit and typed where the language allows. Avoid `any` and
  keep strict checks enabled in TypeScript projects.
- Separate calculations and decisions from persistence, navigation, and external
  calls when doing so makes behavior easier to understand and test.

## 3. Components, content, and presentation

- Review existing components before creating markup; reuse equivalent visual and
  semantic patterns without generalizing prematurely.
- Pages compose components and connect content. Extract blocks that have their
  own responsibility, interaction, or reuse.
- Separate editorial content and business data from presentation; use the
  appropriate CMS, configuration, or fixtures. Internal UI text may live in the
  product's translation mechanism.
- Do not invent real-world information. Clearly identify mocks and placeholders.
- Do not claim an operation saved or sent data when that effect did not occur.
- Keep interaction state local; derive values instead of unnecessarily
  duplicating them in state.

## 4. Design and accessibility

- Centralize shared colors, typography, spacing, and breakpoints in semantic
  tokens. Follow the project's styling solution; do not impose SCSS or BEM.
- Design mobile-first and verify relevant mobile, tablet, and desktop sizes.
- Reserve space for images and asynchronous content to prevent layout shifts.
- Use semantic HTML, labels, visible focus, keyboard support, WCAG AA contrast,
  and appropriately sized touch targets. Respect `prefers-reduced-motion`.
- Do not rely exclusively on hover, color, or animation for essential functions.
- Follow the chosen framework's navigation and rendering conventions.

## 5. Errors, data, and security

- Show clear, safe, actionable errors in the interface language.
- Preserve useful technical context for observability without exposing secrets or
  sensitive data. Do not silence exceptions or report success after a failure.
- Validate permissions and inputs in the server or service acting as the trust
  boundary; browser validation improves UX but does not replace it.
- Do not commit credentials. Use environment-based configuration and examples
  without secrets.
- Expose only the data required for each audience and permission.
- When using owned persistence, protect invariants with constraints and use
  versioned migrations and coherent transactions for related changes.
- When using APIs, keep HTTP semantics, error contracts, and formats consistent;
  coordinate breaking changes and update clients and documentation.

## 6. Dependencies and verification

- Evaluate existing capabilities before adding dependencies.
- Keep manifests and lockfiles consistent; use reproducible installs. Do not edit
  lockfiles manually or apply forced fixes without reviewing their impact.
- Run the relevant available checks: types, lint, build, and tests as appropriate
  to the change. Do not invent commands or claim checks that were not run.
- Add behavioral tests when the risk and logic justify them; cover relevant
  failures and avoid tests that merely restate the implementation.
- Keep tests independent and reproducible, without relying on real data or
  external services unless explicitly set up as integration tests.
- Do not disable checks, hide errors, or lower requirements to get a green result.

## 7. Documentation and delivery

- Update affected documentation with the change. When editing guidelines, review
  the README, area-specific documentation, `docs/`, templates, and existing
  examples.
- Keep one source of truth per rule; summarize and link instead of duplicating.
- Distinguish implemented, proposed, and pending functionality. Document
  contracts, intent, and relevant effects; avoid comments that only restate code.
- Report what changed, why, what was verified, and any remaining limitations or
  placeholders.
- Explicitly note which reviewed documentation did not need changes.

## 8. Git and language

- Follow the Conventional Commits policy at the end of this document.
- Write code and technical identifiers in English. Use the project's explicitly
  chosen language for its documentation and explanations.
- Adapt user-facing text to the product's languages.
- Follow the branching and pull request strategy below. Each project defines its
  specific checks and deployment process.

## Conventional Commits

- All commits must follow [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/).
- The required header format is `<type>[optional scope]: <description>`.
- Use `feat` for a new feature or component and `fix` to correct a defect. Types
  such as `refactor`, `docs`, `test`, `build`, `ci`, and `chore` are also allowed
  when they better describe the intent.
- The scope should be a short, lowercase noun, using hyphens for multiple words,
  for example `feat(contact-details): ...`.
- The description should be brief, specific, in the imperative present tense,
  and without a final period, for example:
  `feat(contact-details): add reusable contact channel component`.
- The message should explain the intent, not just name the file. Add a body
  separated by a blank line when context is needed.
- Breaking changes must use `!` before `:` or a `BREAKING CHANGE: ...` footer,
  as specified.
- Before committing, group files by responsibility so each commit is coherent
  and can be reviewed or reverted independently.

## Branching strategy and pull requests

- `main`: stable version and official production source. The project must state
  whether a merge triggers an automatic deployment; do not assume one.
- `develop`: integration branch for work targeting the next release.
- Do not commit directly to, force-push to, or delete `main` or `develop`.
  Integrate changes through pull requests and applicable validations.
- `feature/*`: features; branch from and merge back into `develop`.
- `bug/*`: non-urgent fixes; branch from and merge back into `develop`. Use this
  prefix consistently; do not alternate with `bugs/*` or `fix/*`.
- `hotfix/*`: urgent production fixes; branch from and merge into `main`, then
  synchronize back to `develop` through a pull request.
- `release/*`: release stabilization from `develop`; include only fixes,
  documentation, and configuration needed to publish. Merge into `main`,
  synchronize back to `develop`, and tag when appropriate.
- Do not keep permanent release branches. Delete temporary branches after merge
  when safe.
- An independent production feature may exceptionally branch from `main` when
  `develop` contains incomplete work. Document the reason in the PR and later
  synchronize `main` back to `develop`.
- A project may explicitly adopt a simpler workflow in its guidelines; do not
  create branches or infrastructure without an operational need.
- PRs use a Conventional Commits title and the repository template. Explain the
  problem, result, validation, and relevant risks; omit sections that do not
  apply. Do not mark checks that were not run.
- Prefer squash merging for work branches. Preserve history when it adds value,
  especially for synchronization of permanent branches.
- Resolve conversations and run relevant checks before merging. Configure branch
  protection when available; do not assume it exists.
- When the user confirms that a PR to `develop` was approved and merged,
  automatically switch the local repository to `develop`, update it with
  fast-forward, and delete the source local branch if it is temporary
  (`feature/*`, `bug/*`, or legacy `fix/*`). Do not ask for additional
  confirmation for this cleanup. Preserve and report uncommitted local changes
  that prevent it; do not delete the remote branch unless explicitly requested.
- Review compatibility, secrets, migrations, and rollback before production as
  appropriate to the scope. Do not merge incomplete work in a PR targeting `main`.

## Agent reading and adoption

- Every agent must read its entry-point file, the project guidelines, and this
  complete base before development. Instructions apply according to their priority.
- Projects must pin the revision of this base using a full commit SHA. Read the
  file from a local checkout at that revision or retrieve its complete contents
  at the pinned revision; a link alone does not count as having read it.
- If the base is unavailable, report the limitation and request access or a
  verified copy before implementing. Do not assume its contents are remembered.
- Project-specific rules complement this base. Record any explicit adaptation,
  its reason, and scope; do not silently alter the shared rule.
- Update the pinned revision through a reviewable change and check its impact on
  project-specific guidelines; do not automatically follow a mutable branch.
