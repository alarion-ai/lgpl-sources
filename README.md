# Alarion LGPL corresponding source

Alarion's macOS app ships libraries licensed under the GNU Lesser General Public License (LGPL),
both inside the app itself and in the optional components ("packs") it installs. This repository
makes the corresponding source of every LGPL component we ship freely available, with no sign-in
required.

## Layout

- `packs/<pack>/<version>/` — one directory per published pack version: a `README.md` listing
  its LGPL components and an `index.json` with each component's exact conda-forge build, the
  feedstock commit it was built from, its upstream source archive (with sha256) and the files it
  contributes to the pack.
- `app/<component>/<version>/` — LGPL libraries that ship inside the application itself rather than in
  a pack (today: the libvips bundle behind the app's image handling, tag `sharp-libvips-<version>`): a
  `README.md`, an `index.json` (exact versions, sha256s, how each archive was checked against its
  upstream's published checksum), `source/` (upstream source archives) and `recipe/` (the build
  scripts and patches that produce the shipped binary).
- `packages/<name>-<version>-<build>/` — one directory per exact conda-forge build:
  - `source/` — the upstream source archive that build used, checksum-verified
  - `recipe/` — the complete conda-forge recipe for that build: build scripts, patches and
    variant configuration
  - `licenses/`, `about.json`, `index.json`, `source.json` — the package's licence files and metadata

Each published pack version also has a git tag, `<pack>-<version>`, so the link shipped in the app
always resolves to exactly what that version contained.

## Rebuilding

- **Pack components** (`packs/`, `packages/`) are unmodified conda-forge builds. To rebuild one,
  use its recipe with conda-forge's tooling (`conda-build` for `meta.yaml`, `rattler-build` for
  `recipe.yaml`), or extract `source/`, apply the patches the recipe lists, and follow its
  `build.sh`. You may replace an LGPL library in an installed Alarion pack with your own modified
  build of it.
- **App components** (`app/`) are not conda-forge builds. Each one's `README.md` gives its own
  build recipe and the steps to run Alarion with your own build of the library, including
  re-signing the app.

## How this is generated

Alarion's build tooling generates this repository:

- `scripts/packs/lgpl-sources.sh` reads a published pack, matches every binary in it to the
  conda-forge build that produced it by Mach-O UUID, and collects the source and recipe of each
  LGPL one.
- `scripts/packs/lgpl-sources-libvips.mjs` publishes `app/sharp-libvips/`. It checks the libvips
  bundle the app ships against the app's lockfile and against the sharp-libvips build recipe, and
  checks each source archive against its upstream's published checksum.

Questions: open an issue in this repository.
