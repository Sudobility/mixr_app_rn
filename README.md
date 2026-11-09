# mixr_app_rn

Repository for **Mixr** (bundle id `com.sudobility.mixr`), a planned React Native app in
the Sudobility app fleet.

> **Status: early scaffold — no application source yet.** This repo currently contains
> only the dependency manifest, the GitHub Packages registry config, and the App Store
> publishing toolkit config. There is **no `App.tsx`/`index.js`, no `app.json`, no
> `ios/`/`android/`/`macos/`/`windows/` native projects, and no Metro/Babel/TypeScript/
> ESLint/Jest config**. The sections below describe what is actually present. See
> [Roadmap / fleet pattern](#roadmap--fleet-pattern) for where it is headed.

## What is here

```
package.json         name-less manifest: version 0.0.8, 2 deps, one "store" script
.npmrc               @sudobility scope → GitHub Packages registry
bun.lock             Bun lockfile (package manager is Bun)
scripts/store.sh     wrapper that runs the shared app_store "store" orchestrator
app_store/           App Store / Google Play / Microsoft Store metadata + screenshot config
```

Dependencies (`package.json`):

- `@sudobility/components-rn` — the shared React Native UI component library / design
  system (installed from GitHub Packages).
- `@react-native-segmented-control/segmented-control`

## Prerequisites

- [Bun](https://bun.sh) (this repo uses `bun.lock`; do not use npm/yarn/pnpm).
- A **GitHub Packages** read token. The `@sudobility/*` dependencies resolve from
  `https://npm.pkg.github.com` (see `.npmrc`: `@sudobility:registry=https://npm.pkg.github.com`).
  Before installing, add a line to your `~/.npmrc`:

  ```
  //npm.pkg.github.com/:_authToken=<token with read:packages>
  ```

## Install

```bash
bun install
```

## Build / test / run

There is **no app entry point, native project, or build/test/lint tooling in this repo
yet**, so there is nothing to build, test, lint, or launch. `package.json` defines a
single script:

```bash
bun run store      # → scripts/store.sh → shared workflows/app_store "store" orchestrator
```

`scripts/store.sh` requires the shared toolkit checked out at `~/projects/workflows/app_store`
(override with `WORKFLOWS_DIR`), and uses `app_store/` in this repo for metadata (override
the config dir with `APP_STORE_DIR`). See the `workflows/app_store` README for subcommands
(e.g. `--screenshots:iphone:en`, `--submit:appstore`). Because there is no built app yet,
`store` can only be exercised once native projects exist.

## App Store config (`app_store/`)

Metadata for the shared publishing toolkit. Most consumer-facing fields are placeholders
(`TODO`) and must be filled before a real submission.

- `info.json` — app identity (`Mixr`, `com.sudobility.mixr`), declared iOS build target
  (`Mixr.xcworkspace` / scheme `Mixr`, Metro port `8081`), store categories/pricing, min
  iOS 15.1. The referenced Xcode workspace does not exist in this repo yet.
- `screens.json` — simulator/emulator + resolution matrix for screenshots.
- `languages.json` — target localization languages for store metadata.
- `paths.json` / `screens.json` under `screenshots/info/en/` — screenshot capture routes
  and captions (one caption per path).
- `.env.example` — Apple / Google Play / Microsoft Partner Center credentials template
  (copy to `app_store/.env`; `.env` and `.keys/` are gitignored).

## Roadmap / fleet pattern

Mixr is part of a fleet of sibling React Native apps under `~/projects/*_app_rn`
(e.g. `music_app_rn`, `genuivo_app_rn`, `sudojo_app_rn`). Those apps establish the
intended shape this repo will grow into — bare React Native 0.83 (no Expo), React 19,
Bun, NativeWind 4 + Tailwind, and the shared `@sudobility/*` libraries — but **none of
that is wired up here yet**, so this README does not document commands or architecture
that do not exist in this repo. Consult a sibling app for the current conventions when
scaffolding Mixr's source.

## License

Private (not published).
