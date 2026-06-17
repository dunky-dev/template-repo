# Agent + contributor guide

The working contract for anyone (human or agent) modifying code in this
repo. This file is the canonical entry point — read it first, every time.

## Preflight

Before touching any code, read these in order:

1. `AGENTS.md` (this file) — rules, boundaries, workflow.
2. `README.md` — what this project is and how to run it.
3. `ARCHITECTURE.md` — the structure and where things live.

If a per-package `AGENTS.md` exists alongside a `package.json`, read it
before editing files in that package — it overrides anything here for
that scope.

## Boundaries

<!-- Encode this repo's hard invariants here — the rules that are not
preferences but must hold for the design to stay coherent (e.g. layering,
dependency direction, what may import what). Delete this comment once filled. -->

## Workflow

Before merging, walk this checklist:

1. **Do tests reflect the change?** Behavior added or changed must be
   exercised by a test under the package's `tests/`.
2. **Is it green?** `pnpm lint`, `pnpm typecheck`, `pnpm test`,
   `pnpm format:check`, and `pnpm knip` all pass.
3. **Did you record a changeset?** If the change affects a published
   package, run `pnpm changeset` so the release flow can version it.

## Diagrams in docs

Draw ASCII diagrams (boxes, trees, flows) with plain `|`, `-`, and `+`
only — never Unicode box-drawing characters (`┌ ┐ └ ┘ ─ │ ├ ┼ ▼` …).
Use `|` for verticals, `-` for horizontals, `+` for every corner and
junction, and a plain `v` / `^` / `>` / `<` for arrowheads. The
box-drawing glyphs render inconsistently across fonts, terminals, and
GitHub, and are awkward to edit; the ASCII set is portable and diffs
cleanly. This applies to every `.md` in the repo.

## Per-package guidance

If a package needs rules of its own (build quirks, platform-only
constraints), add an `AGENTS.md` next to its `package.json`. The same
convention applies further down the tree — anywhere a directory has
rules its parent doesn't capture.

Resolution is nearest-wins: an `AGENTS.md` inside the directory you
are editing (or any ancestor up to the repo root) overrides everything
above it for that directory's code. When editing a file, read every
`AGENTS.md` between the repo root and that file, apply them top-down,
and let the closest one settle conflicts.

Keep nested files small. Only encode what genuinely differs from the
ancestor — duplicating rules invites drift. If a nested file would
just restate the root, delete it.
