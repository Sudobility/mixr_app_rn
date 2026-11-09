# mixr_app_rn

> **Git: never auto-commit or auto-push.** Leave work in the working tree; run
> `git commit`/`push`/`gh pr create` only when the user explicitly asks in that turn.
> Stay on the current branch.

**Status: pre-source scaffold.** Mixr (`com.sudobility.mixr`) is a planned React Native
app in the Sudobility fleet. This repo currently has **no application code**. Do not
assume an app exists here — verify before claiming otherwise.

## What actually exists (verified)

Tracked files (`git ls-files`): `package.json`, `.npmrc`, `.gitignore`,
`.gitattributes`, `bun.lock`, `scripts/store.sh`, and `app_store/*`. Nothing else.

- **No** `App.tsx`/`index.js`, `app.json`, `src/`, native projects
  (`ios`/`android`/`macos`/`windows`), or `tsconfig`/`babel.config`/`metro.config`/
  `eslint`/`jest`/`vitest` config.
- `package.json` has **no `name` field**, version `0.0.8`, deps
  `@sudobility/components-rn` + `@react-native-segmented-control/segmented-control`,
  and exactly one script: `store`.

## Package manager & registry

- **Bun** (`bun.lock`). Never npm/yarn/pnpm.
- `@sudobility/*` installs from **GitHub Packages** (`.npmrc`:
  `@sudobility:registry=https://npm.pkg.github.com`), NOT npmjs. `bun install` needs
  `//npm.pkg.github.com/:_authToken=<token>` (token with `read:packages`) in `~/.npmrc`.
- Fleet note: `@sudobility/components-rn` is often **dev-synced** (src+dist overlaid into
  `node_modules`) across sibling apps; `bun install`/`bun add` wipe the overlay, so it may
  need re-syncing after install.

## Commands

- `bun install` — dependencies.
- `bun run store` — the only script. → `scripts/store.sh` → shared App Store orchestrator
  at `~/projects/workflows/app_store/store` (override via `WORKFLOWS_DIR`), using this
  repo's `app_store/` for metadata (override via `APP_STORE_DIR`). There is no built app
  yet, so this cannot produce/submit a build until native projects exist.

There are **no** `start`/`ios`/`android`/`typecheck`/`lint`/`test`/`verify` scripts.
Do not invent or run them.

## App Store config (`app_store/`)

Metadata for the shared `workflows/app_store` toolkit. `info.json` declares identity
(`Mixr`, `com.sudobility.mixr`), an intended iOS target (`Mixr.xcworkspace`, scheme
`Mixr`, Metro port `8081`, min iOS 15.1), and store categories. Most store-copy fields
are `TODO` placeholders. The referenced Xcode workspace does not exist here yet.
`app_store/.env` and `app_store/.keys/` are gitignored.

## When adding the app source

Mixr will follow the fleet conventions used by sibling `~/projects/*_app_rn` apps
(bare RN 0.83 / no Expo, React 19, NativeWind 4 + Tailwind, shared `@sudobility/*`
libs, per-app Metro port, `verify` = typecheck + lint + test). **Copy the conventions
from a current sibling** (e.g. `music_app_rn`, `genuivo_app_rn`) rather than inventing
them, and update this file + the README once the real stack and commands land here.
