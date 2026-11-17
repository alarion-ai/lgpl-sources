# @img/sharp-libvips-darwin-arm64 1.3.4 (libvips bundle used by sharp 0.35.5)

Corresponding source for the LGPL-licensed libraries inside `lib/libvips-cpp.8.18.7.dylib`, the prebuilt libvips
shared library that the Alarion macOS app ships through the npm package above. The bundle links
its dependencies statically into that one library, so every library in it is covered by the build
recipe below. The LGPL components are:

| Library | Version | Licence | Source archive | Licence text in the archive | Patches applied by the recipe |
|---|---|---|---|---|---|
| libvips | 8.18.7 | LGPL-2.1-or-later | `source/vips-8.18.7.tar.xz` | `LICENSE` | `recipe/patches/libvips-cpp-soversion.patch` |
| glib | 2.90.0 | LGPL-2.1-or-later | `source/glib-2.90.0.tar.xz` | `COPYING`, `LICENSES/` | `recipe/patches/glib-without-gregex.patch` |
| pango | 1.58.2 | LGPL-2.0-or-later | `source/pango-1.58.2.tar.xz` | `COPYING` | - |
| librsvg | 2.63.2 | LGPL-2.1-or-later | `source/librsvg-2.63.2.tar.xz` | `COPYING.LIB` | `recipe/patches/librsvg-embedded-image-memory-limits.patch` |
| libheif | 1.23.5 | LGPL-3.0-or-later | `source/libheif-1.23.5.tar.gz` | `COPYING` | - |
| libexif | 0.6.26 | LGPL-2.1-or-later | `source/libexif-0.6.26.tar.xz` | `COPYING` | - |
| fribidi | 1.0.17 | LGPL-2.1-or-later | `source/fribidi-1.0.17.tar.xz` | `COPYING` | - |
| proxy-libintl | 0.5 | LGPL-2.0-or-later | `source/proxy-libintl-0.5.tar.gz` | `COPYING` | - |

`index.json` records each archive's sha256 and upstream URL, how it was checked against the
checksum its upstream publishes, each patch's origin URL and sha256, and the exact bundle (npm
integrity, full `versions.json`).

## The library in the app

In the installed app the library is at

    Alarion.app/Contents/Resources/app.asar.unpacked/node_modules/@img/sharp-libvips-darwin-arm64/lib/libvips-cpp.8.18.7.dylib

It is the npm package's library, unmodified except for its code signature: packaging re-signs it
with Alarion's Developer ID, so its sha256 differs from the npm copy's
(`c1a5b5633b21aeb8a229abf7d062e07e4d778c0b44ed43cd1f93362bda58c322`). To check that they are the same library, strip the signature from both and
compare them:

    cp "/Applications/Alarion.app/Contents/Resources/app.asar.unpacked/node_modules/@img/sharp-libvips-darwin-arm64/lib/libvips-cpp.8.18.7.dylib" installed.dylib
    curl -sL https://registry.npmjs.org/@img/sharp-libvips-darwin-arm64/-/sharp-libvips-darwin-arm64-1.3.4.tgz | tar xzf - package/lib/libvips-cpp.8.18.7.dylib
    cp package/lib/libvips-cpp.8.18.7.dylib npm.dylib
    codesign --remove-signature installed.dylib
    codesign --remove-signature npm.dylib
    cmp -l installed.dylib npm.dylib

The only difference is the `vmsize` of the `__LINKEDIT` segment (see `otool -l`), which
follows the size of the signature that was removed.

## Rebuilding the library

`recipe/sharp-libvips-v1.3.4.tar.gz` is the sharp-libvips build at tag `v1.3.4` (commit `158bf3bfb1e11de50032645873d52e5920c26986`).
Build from that tarball: `build.sh`, `build/posix.sh`, `versions.properties`, `platforms/darwin-arm64v8/meson.ini`, `platforms/darwin-arm64v8/Toolchain.cmake`, `LICENSE`, `THIRD-PARTY-NOTICES.md` are also extracted next to it so they can be read on the
web, but they are not the complete tree. On Apple-silicon macOS, with the Xcode command line tools
and Homebrew's pkg-config, meson, ninja and cmake:

    tar xzf sharp-libvips-v1.3.4.tar.gz
    cd sharp-libvips-1.3.4
    ./build.sh darwin-arm64v8

The result is `target/lib/libvips-cpp.8.18.7.dylib` (also packed as `sharp-libvips-darwin-arm64v8.tar.gz`).

`build/posix.sh` downloads every source archive and patch while it runs; it does not read
`source/` or `recipe/patches/`. The copies here are byte-identical to what it downloads (URLs and
sha256s in `index.json`), so if an upstream URL stops working, change the matching `$CURL` line to
read the local copy instead.

The upstream recipe is not fully pinned: it installs the current nightly Rust toolchain through
rustup, regenerates librsvg's Cargo lockfile (`cargo update`), and applies a patch from an open pull
request to libultrahdr (which is not LGPL). A later rebuild can therefore fail or differ in its
non-LGPL parts. If it fails, pin Rust to a nightly from around the tag's date (edit the
`--default-toolchain nightly` line in `build/posix.sh`, e.g. to `nightly-YYYY-MM-DD`).

## Running Alarion with your own build

macOS checks the app's code signature, so after replacing the library you must re-sign the app;
otherwise macOS reports it as damaged and refuses to open it. The app accepts libraries that are
not signed by Alarion (it has the `com.apple.security.cs.disable-library-validation` entitlement), so an
ad-hoc signature is enough:

1. Quit Alarion and copy it somewhere you can edit it (macOS blocks changes inside an app in
   `/Applications` unless your terminal has the App Management permission in System Settings >
   Privacy & Security):

       ditto /Applications/Alarion.app ~/Alarion-custom.app

2. Replace the library with your build:

       cp target/lib/libvips-cpp.8.18.7.dylib ~/Alarion-custom.app/Contents/Resources/app.asar.unpacked/node_modules/@img/sharp-libvips-darwin-arm64/lib/

3. Re-sign the whole app ad-hoc, keeping its entitlements:

       codesign --force --deep --sign - --preserve-metadata=entitlements ~/Alarion-custom.app

4. Open `~/Alarion-custom.app`. sharp loads your library when the app starts.

Do steps 2 and 3 before you first open the copy: once macOS has run an app it protects that copy
against changes too. The copy is signed by you, not by Alarion, so it will not receive Alarion's
automatic updates.

The build scripts (`recipe/`) are Apache-2.0 (`recipe/LICENSE`).
