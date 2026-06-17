# chimba-ui template repo

A pnpm-workspace monorepo starter with the shared chimba-ui tooling baked in.
Use it as a GitHub **template repository** (_Use this template_) or copy it with
`npx degit chimba-ui/template-repo my-new-repo`.

## What's included

| Tool            | File                            | Purpose                                                                                  |
| --------------- | ------------------------------- | ---------------------------------------------------------------------------------------- |
| **oxlint**      | `.oxlintrc.json`                | Linting (eslint/import/react/unicorn/vitest plugins).                                    |
| **oxfmt**       | `.oxfmtrc.json`                 | Formatting — house style: no semicolons, single quotes, width 100, kebab-case filenames. |
| **lint-staged** | `.lintstagedrc.json`            | Runs `oxlint --fix` + `oxfmt` on staged `*.{ts,tsx}`.                                    |
| **husky**       | `.husky/pre-commit`             | Runs lint-staged before each commit. Installed via the `prepare` script.                 |
| **knip**        | `knip.config.ts`                | Unused-export/dependency detection (minimal config — extend per package).                |
| **TypeScript**  | `tsconfig.json`                 | Strict, ESM, bundler resolution. One `@chimba-ui/core` path alias.                       |
| **Vitest**      | `vitest.config.ts`              | Node test environment.                                                                   |
| **pnpm**        | `.npmrc`, `pnpm-workspace.yaml` | Workspace tuning; packages live under `packages/**`.                                     |
| **CI**          | `.github/workflows/ci.yml`      | Lint + typecheck + test on push/PR (Node 24, pnpm 10.20.0).                              |

## Per-repo setup after scaffolding

1. **Rename the root package** in `package.json` (`name`).
2. **Rename the placeholder package** `packages/core` → your real package(s):
   - update its `package.json` `name` (`@chimba-ui/<thing>`),
   - add a matching alias in `tsconfig.json` `paths`,
   - replace `packages/core/src/index.ts` with the real public API.
3. **Add React if needed** — the template ships without it. For a React package,
   `pnpm add -w -D react @types/react`, then uncomment the `ignoreDependencies`
   line in `knip.config.ts` so knip doesn't flag the root-level peers.
4. **Adjust `knip.config.ts`** further — add per-package `ignoreDependencies` for
   packages that re-export another's surface without importing it directly.
5. `pnpm install` — this also activates husky hooks via `prepare`.

## Conventions inherited from state-machine

- **Filenames are kebab-case** (enforced by `unicorn/filename-case`).
- **Package source files may not use default exports** (`import/no-default-export`
  on `packages/**/src/**`) — use named exports for public API.
- **Worktrees** for parallel work: create as a sibling dir and run `pnpm install`
  in each (worktrees don't share `node_modules`).

## License

[MIT](./LICENSE)
