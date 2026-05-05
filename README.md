# bluecorn.github.io

The static site at https://bluecorn.github.io, built with [Jaspr](https://jaspr.site) in static mode.

## Setup

Requires [FVM](https://fvm.app). After cloning:

```sh
git submodule update --init        # populates upstream/jaspr (reference only)
fvm install                         # installs the SDK declared in .fvmrc
fvm dart pub get
```

## Develop

```sh
fvm dart run jaspr_cli:jaspr serve
```

Dev server runs at http://localhost:8080.

## Build

```sh
fvm dart run jaspr_cli:jaspr build
```

Output goes to `build/jaspr/`.

## Deploy

`git push origin main` triggers `.github/workflows/deploy.yml`, which builds the site and publishes to GitHub Pages.

## `upstream/jaspr`

Submodule pinned to the upstream Jaspr repo, kept locally for development reference. Excluded from CI by `submodules: false` in the deploy workflow and never appears in the published artifact.
