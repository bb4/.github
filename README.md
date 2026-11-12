# bb4

Decades of Scala simulations, puzzles, and games — see [barrybecker4.org](https://barrybecker4.org).

## Reusable workflows

| Workflow | Purpose |
|---|---|
| [`bb4-ci.yml`](.github/workflows/bb4-ci.yml) | Shared Gradle CI (Temurin 25, Gradle User Home cache, optional publish / downstream dispatch) |
| [`jpackage-release.yml`](.github/workflows/jpackage-release.yml) | Multi-OS native installers via `jpackageAllApps` |

### `bb4-ci` caller example

```yaml
name: CI

on:
  push:
    branches: [ master, main ]
  pull_request:
  repository_dispatch:
    types: [ upstream-updated ]

jobs:
  build:
    uses: bb4/.github/.github/workflows/bb4-ci.yml@main
    with:
      gradle-args: build
      publish: true
      notify-downstream: true   # libraries that fan out rebuilds
      # use-xvfb: true          # e.g. bb4-simulations
      # extra-gradle-args: -Djava.awt.headless=true
      # publish-gradle-args: --max-workers=1 --no-parallel   # multi-artifact Central rate limits
    secrets:
      OSSRH_USERNAME: ${{ secrets.OSSRH_USERNAME }}
      OSSRH_PASSWORD: ${{ secrets.OSSRH_PASSWORD }}
      BB4_DISPATCH_TOKEN: ${{ secrets.BB4_DISPATCH_TOKEN }}
```

Inputs default to a quiet `./gradlew build` (no `--info`). On `repository_dispatch`, the workflow runs `clean … --refresh-dependencies` unless `refresh-on-dispatch: false`.

### Downstream dispatch map

[`downstream-dispatch.json`](downstream-dispatch.json) maps a producer repo name to the repos that should receive `upstream-updated` when that producer publishes from `main`/`master`. Edit that file instead of hardcoding lists in each CI workflow.

## Build status

| Repo | Status |
|---|---|
| bb4-gradle | ![bb4-gradle](https://github.com/bb4/bb4-gradle/actions/workflows/ci.yml/badge.svg) |
| bb4-project-template | ![bb4-gradle](https://github.com/bb4/bb4-project-template/actions/workflows/ci.yml/badge.svg) |
| bb4-common | ![bb4-common](https://github.com/bb4/bb4-common/actions/workflows/ci.yml/badge.svg) |
| bb4-math | ![bb4-math](https://github.com/bb4/bb4-math/actions/workflows/ci.yml/badge.svg) |
| bb4-ui | ![bb4-ui](https://github.com/bb4/bb4-ui/actions/workflows/ci.yml/badge.svg) |
| bb4-sound | ![bb4-sound](https://github.com/bb4/bb4-sound/actions/workflows/ci.yml/badge.svg) |
| bb4-A-star | ![bb4-A-star](https://github.com/bb4/bb4-A-star/actions/workflows/ci.yml/badge.svg) |
| bb4-optimization | ![bb4-optimization](https://github.com/bb4/bb4-optimization/actions/workflows/ci.yml/badge.svg) |
| bb4-expression | ![bb4-expression](https://github.com/bb4/bb4-expression/actions/workflows/ci.yml/badge.svg) |
| bb4-shortest-paths | ![bb4-shortest-paths](https://github.com/bb4/bb4-shortest-paths/actions/workflows/ci.yml/badge.svg) |
| bb4-imageproc | ![bb4-imageproc](https://github.com/bb4/bb4-imageproc/actions/workflows/ci.yml/badge.svg) |
| bb4-adventure | ![bb4-adventure](https://github.com/bb4/bb4-adventure/actions/workflows/ci.yml/badge.svg) |
| bb4-aikido-app | ![bb4-aikido-app](https://github.com/bb4/bb4-aikido-app/actions/workflows/ci.yml/badge.svg) |
| bb4-Q-learning | ![bb4-Q-learning](https://github.com/bb4/bb4-Q-learning/actions/workflows/ci.yml/badge.svg) |
| bb4-experimentation | ![bb4-experimentation](https://github.com/bb4/bb4-experimentation/actions/workflows/ci.yml/badge.svg) |
| bb4-discrete-optimization | ![bb4-discrete-optimization](https://github.com/bb4/bb4-discrete-optimization/actions/workflows/ci.yml/badge.svg) |
| bb4-puzzles | ![bb4-puzzles](https://github.com/bb4/bb4-puzzles/actions/workflows/ci.yml/badge.svg) |
| bb4-simulations | ![bb4-simulations](https://github.com/bb4/bb4-simulations/actions/workflows/ci.yml/badge.svg) |
| bb4-games | ![bb4-games](https://github.com/bb4/bb4-games/actions/workflows/ci.yml/badge.svg) |
| bb4-color-mixer | ![bb4-color-mixer](https://github.com/bb4/bb4-color-mixer/actions/workflows/ci.yml/badge.svg) |
| bb4-traffic-simulation | ![bb4-traffic-simulation](https://github.com/bb4/bb4-traffic-simulation/actions/workflows/ci.yml/badge.svg) |
