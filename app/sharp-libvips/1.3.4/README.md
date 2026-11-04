# @img/sharp-libvips-darwin-arm64 1.3.4 (libvips bundle used by sharp 0.35.5)

Corresponding source for the LGPL-licensed libraries inside `lib/libvips-cpp.8.18.7.dylib` (sha256
`c1a5b5633b21aeb8a229abf7d062e07e4d778c0b44ed43cd1f93362bda58c322`), the prebuilt libvips shared library that the Alarion macOS app ships
unmodified through the npm package above. The bundle links its dependencies statically into that
one library, so every library in it is covered by the build recipe below; the LGPL components are:

| Library | Version | Licence | Source archive | Patches applied by the recipe |
|---|---|---|---|---|
| libvips | 8.18.7 | LGPL-2.1-or-later | `source/vips-8.18.7.tar.xz` | `recipe/patches/libvips-cpp-soversion.patch` |
| glib | 2.90.0 | LGPL-2.1-or-later | `source/glib-2.90.0.tar.xz` | `recipe/patches/glib-without-gregex.patch` |
| pango | 1.58.2 | LGPL-2.0-or-later | `source/pango-1.58.2.tar.xz` | - |
| librsvg | 2.63.2 | LGPL-2.1-or-later | `source/librsvg-2.63.2.tar.xz` | `recipe/patches/librsvg-embedded-image-memory-limits.patch` |
| libheif | 1.23.5 | LGPL-3.0-or-later | `source/libheif-1.23.5.tar.gz` | - |
| libexif | 0.6.26 | LGPL-2.1-or-later | `source/libexif-0.6.26.tar.xz` | - |
| fribidi | 1.0.17 | LGPL-2.1-or-later | `source/fribidi-1.0.17.tar.xz` | - |
| proxy-libintl | 0.5 | LGPL-2.0-or-later | `source/proxy-libintl-0.5.tar.gz` | - |

`index.json` carries each archive's sha256, how it was checked against the checksum its upstream
publishes, and the exact bundle (npm integrity, full `versions.json`). Each source archive
contains its own licence texts (`COPYING`).

## Rebuilding / replacing the library

`recipe/` is the sharp-libvips build at tag `v1.3.4` (commit `158bf3bfb1e11de50032645873d52e5920c26986`):
`build/posix.sh` downloads these same upstream archives (the URLs are listed in `index.json`),
applies the patches in `recipe/patches/` and builds the static libraries and the final
`libvips-cpp` shared library. On Apple-silicon macOS, extract `sharp-libvips-v1.3.4.tar.gz`
and run `./build.sh darwin-arm64v8` (Xcode command line tools, Homebrew pkg-config, meson, cmake,
a Rust toolchain; librsvg's Rust crates are fetched by cargo and are not LGPL). To use your own
build, replace `lib/libvips-cpp.8.18.7.dylib` inside the installed app's unpacked
`node_modules/@img/sharp-libvips-darwin-arm64/lib/` with it; the app loads it through sharp at start-up.

The build scripts (`recipe/`) are Apache-2.0 (`recipe/LICENSE`).
