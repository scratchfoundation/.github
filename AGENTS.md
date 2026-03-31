# Agent Guide: Scratch Repositories (Template)

This file is a template for `AGENTS.md` files across Scratch repositories. Copy it to the root of a repo and
replace the placeholder sections with repo-specific content. The HTML comments are standing instructions for
whoever adapts the template — they are safe to leave in place.

When adapting this template, consider adding sections for **Repository layout** and any language- or
framework-specific conventions (TypeScript guidelines, React patterns, testing conventions, etc.) that are
non-obvious from the code itself.

---

## AI-assisted development policy

See [CONTRIBUTING.AI.md](https://github.com/scratchfoundation/.github/blob/main/CONTRIBUTING.AI.md) for Scratch's
org-wide policy on AI-assisted contributions. The short version: human developers remain responsible for all code
they submit. Do not submit code you cannot explain and defend in a review.

## Agent defaults

Use these defaults unless the user asks otherwise:

1. Keep changes minimal and scoped to the user request. Do not refactor surrounding code, add features, or clean up
   style in areas you weren't asked to touch.
2. Do not preserve backward compatibility when it isn't required. Shims, aliases, and legacy signatures add
   maintenance burden without benefit when all callers are internal — just update the call sites. When a package
   is published to npm or otherwise consumed by external callers, treat its public API as a contract and preserve
   compatibility unless explicitly told otherwise.
3. Write comments that explain the current code, not its history. Do not reference prior implementations,
   intermediate states, or what the code "used to do." If an approach seems counterintuitive, explain why it is
   correct now — not why it changed.
4. Prefer fixing root causes over adding surface-level workarounds or assertions.
5. When fixing a bug, start by adding one or more failing tests that reproduce it, then implement the fix. Iterate
   until all tests pass, including but not limited to the new tests.
6. When adding runtime guards for states that should never happen, log actionable context (function name, relevant
   IDs, key flags) rather than failing silently. Use `console.warn` for recoverable states and `console.error` for
   invalid required data (or your repo's logger equivalent, if one exists).
7. Preserve failure semantics when refactoring. An implicit crash (null dereference, `!` assertion) should become
   an explicit `throw` with a useful message — not silent failure. Code that previously wouldn't crash still
   shouldn't, but consider whether a warning is warranted. Replacing a potential null dereference with
   `if (!foo) return` could make a bug harder to find; `if (!foo) throw new Error(...)` surfaces it.
8. Do not add error handling, fallbacks, or validation for scenarios that cannot happen. Trust internal code and
   framework guarantees. Only validate at system boundaries (user input, external APIs).

## What this repository is

<!--
  When adapting this template: replace the content of this section with a 2–4 sentence description of the repo —
  what it does, what it produces, and how it fits into the broader Scratch ecosystem.
-->

This is the [`.github` repository](https://github.com/scratchfoundation/.github) for the `scratchfoundation` GitHub
organization. It provides org-wide GitHub defaults:

- `profile/README.md` — the organization profile shown at [github.com/scratchfoundation](https://github.com/scratchfoundation/)
- `CONTRIBUTING.md` — default contributing guidelines inherited by repos that don't define their own
- `CONTRIBUTING.AI.md` — Scratch's org-wide policy on AI-assisted development
- `PULL_REQUEST_TEMPLATE.md` — default PR template
- `AGENTS.md` (this file) — template for per-repo agent guides

There is no build step and no test suite. Changes here are prose and Markdown only.

## Build and lint

<!--
  When adapting this template: replace the content of this section with the actual commands for this repo.
  If the repo has no build step or test suite, remove this section or replace it with a brief note.
  Example shape:

  ```sh
  npm run build        # Compile and bundle
  npm start            # Start dev server
  npm run test         # Full check: lint + build + unit tests
  npm run test:lint    # Lint only
  npm run test:unit    # Unit tests only
  ```

  Run `npm run test:lint` first when iterating — it is fast. Run `npm run test` before declaring work done.
-->

*This repository has no build step or test suite — see "What this repository is" above.*

## Technology defaults

The following apply to new code and to migrations. Repo-specific `AGENTS.md` files may override them. These
standards are also documented in
[CONTRIBUTING.md](https://github.com/scratchfoundation/.github/blob/main/CONTRIBUTING.md) for human contributors.

- **Language**: Use TypeScript. Use JavaScript only when the package is not yet configured for TypeScript (e.g.,
  `scratch-www`) or if there is some other overriding reason.
- **Linting**: Use [`eslint-config-scratch`](https://github.com/scratchfoundation/eslint-config-scratch) for all
  JS/TS code.
- **Bundler**: Use Vite for new repos. Migrate from webpack to Vite as time allows.
- **Test framework**: Use Vitest for new packages. Existing packages may use Jest or Tap; follow whatever is
  already in use unless migrating.
- **Commit messages**: Use [Conventional Commits](https://www.conventionalcommits.org/) style as understood by
  `semantic-release` (e.g., `feat:`, `fix:`, `chore:`). Not all repos enforce this automatically, but follow the
  convention regardless.
- **Browser targets**: Target [Baseline Widely Available](https://web.dev/baseline) for browser code. Do not use
  features outside that set without calling it out explicitly, and do not add polyfills for features already
  within it.

## Branching

Base new branches on the repo's primary integration branch: `develop` if it exists, otherwise `main` or `master`.
Check which exists before creating a branch — do not assume.

## Dependencies and bundling

Scratch packages serve multiple consumers: internal (e.g., scratch-www loading scratch-gui), automated tests
(often in Node), and third parties using individual packages standalone.

**`peerDependencies` + externalize in bundle**: packages that are part of this package's public interface, or
where two copies in the same application would cause runtime errors. React and ReactDOM are the primary example —
any package that exports React components must list them as peer dependencies so the consuming app shares one
React instance. Always externalize peer dependencies in the bundle.

**`dependencies`**: packages this package owns as private implementation details. Consumers don't need to know
they exist. For example, `scratch-vm` is a dependency of `scratch-gui` — an application package like `scratch-www`
loads `scratch-gui` without needing to declare or know about `scratch-vm`.

**`devDependencies`**: anything only needed during development, build, or testing.

**Bundling by package type**:

- *Application packages* (`scratch-www`, `scratch-desktop`): bundle everything into the final output.
- *Library packages*: externalize peer dependencies; bundle regular dependencies.

**Migration**: many existing repos don't yet follow these rules. For established repos, drift toward this pattern
incrementally rather than mass-refactoring.

## npm workflow

Use `npm ci` to install existing dependencies so you get the exact versions in `package-lock.json`.

When adding or updating a dependency, run `npm install some-package@version` to update both `package.json` and
`package-lock.json` together.

Keep each section of `package.json` (e.g., `dependencies`, `devDependencies`, `scripts`) in alphabetical order.

## Before submitting changes

<!--
  When adapting this template: add or remove checklist items to match this repo. Repos with a build step and
  test suite should include:
  - **Build passes**: `npm run build` completes successfully.
  - **Tests pass**: `npm run test` completes with no failures.
  - **No lint errors**: `npm run test:lint` passes.
-->

Review all changes and confirm:

- **Scope**: Changes are confined to the user request; nothing extra was added or modified.
- **Correctness**: Logic is sound and edge cases were considered.
- **Comments**: Comments are necessary, short, and clear; self-explanatory code has none.
- **Simplicity**: Implementation is as simple as possible; no speculative abstractions remain.
- **Documentation**: Update `AGENTS.md` and any other documentation files whose content is affected by the change
  (commands, repo structure, conventions, etc.).
