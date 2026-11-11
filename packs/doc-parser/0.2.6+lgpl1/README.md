# doc-parser 0.2.6+lgpl1: LGPL corresponding source

The Alarion `doc-parser` pack, version `0.2.6+lgpl1` (sha256 `cc76465e76f7859f487b39290a490c501f3f22c591da6155ad86f1d8f844f75f`), ships the
LGPL-licensed components below as unmodified conda-forge binaries. For each one this repository
holds the exact upstream source archive the conda-forge build used and the full conda-forge
recipe for that build (build scripts, patches, variant configuration), under the directory listed.
Alarion did not modify these components. To rebuild one, run its recipe with conda-forge's
tooling, or apply its patches to the source and follow its `build.sh`.

| Component | Version | conda-forge build | Licence declared by conda-forge | Source and recipe |
|---|---|---|---|---|
| cairo | 1.18.6 | `h580cee5_0` | LGPL-2.1-only or MPL-1.1 | [`packages/cairo-1.18.6-h580cee5_0`](../../../packages/cairo-1.18.6-h580cee5_0) |
| ffmpeg | 9.0.2 | `lgpl_h1d9c18f_5` | LGPL-2.1-or-later | [`packages/ffmpeg-9.0.2-lgpl_h1d9c18f_5`](../../../packages/ffmpeg-9.0.2-lgpl_h1d9c18f_5) |
| fribidi | 1.0.18 | `hb001647_0` | LGPL-2.1-or-later | [`packages/fribidi-1.0.18-hb001647_0`](../../../packages/fribidi-1.0.18-hb001647_0) |
| gdk-pixbuf | 2.44.8 | `h5867e2c_2` | LGPL-2.1-or-later | [`packages/gdk-pixbuf-2.44.8-h5867e2c_2`](../../../packages/gdk-pixbuf-2.44.8-h5867e2c_2) |
| graphite2 | 1.3.15 | `h784d473_1` | LGPL-2.0-or-later | [`packages/graphite2-1.3.15-h784d473_1`](../../../packages/graphite2-1.3.15-h784d473_1) |
| lame | 4.0 | `hef9b5c2_1` | LGPL-2.0-only | [`packages/lame-4.0-hef9b5c2_1`](../../../packages/lame-4.0-hef9b5c2_1) |
| libglib | 2.90.0 | `hccd281b_0` | LGPL-2.1-or-later | [`packages/libglib-2.90.0-hccd281b_0`](../../../packages/libglib-2.90.0-hccd281b_0) |
| libiconv | 1.18 | `he4c29f2_3` | LGPL-2.1-only | [`packages/libiconv-1.18-he4c29f2_3`](../../../packages/libiconv-1.18-he4c29f2_3) |
| libintl | 0.25.1 | `hae62183_2` | LGPL-2.1-or-later | [`packages/libintl-0.25.1-hae62183_2`](../../../packages/libintl-0.25.1-hae62183_2) |
| libpango | 1.58.2 | `hc2ac4f2_3` | LGPL-2.1-or-later | [`packages/libpango-1.58.2-hc2ac4f2_3`](../../../packages/libpango-1.58.2-hc2ac4f2_3) |
| libplacebo | 7.360.1 | `h8466173_2` | LGPL-2.1-or-later | [`packages/libplacebo-7.360.1-h8466173_2`](../../../packages/libplacebo-7.360.1-h8466173_2) |
| librsvg | 2.62.4 | `hc8ac265_0` | LGPL-2.1-or-later | [`packages/librsvg-2.62.4-hc8ac265_0`](../../../packages/librsvg-2.62.4-hc8ac265_0) |
| mpg123 | 1.33.7 | `h0e3f465_1` | LGPL-2.1-only | [`packages/mpg123-1.33.7-h0e3f465_1`](../../../packages/mpg123-1.33.7-h0e3f465_1) |

The FFmpeg libraries are built `--disable-gpl --enable-version3` and report "LGPL version 3
or later" in their own binaries (`ffmpeg -L`); that, not conda-forge's metadata, is their licence.

The binaries each component contributes to the pack, and the conda-forge feedstock commit
each was built from, are listed in `index.json`.
