# doc-parser 0.2.6+lgpl2: LGPL corresponding source

The Alarion `doc-parser` pack, version `0.2.6+lgpl2` (sha256 `a2550f46b426c4cb79c357133b6df1b8bb6ae7582a46b8ff95edfbf5c6e161ad`), ships the
LGPL-licensed components below as unmodified conda-forge binaries. For each one this repository
holds the exact upstream source archive the conda-forge build used and the full conda-forge
recipe for that build (build scripts, patches, variant configuration), under the directory listed.
Alarion did not modify these components. To rebuild one, run its recipe with conda-forge's
tooling, or apply its patches to the source and follow its `bld.bat`.

| Component | Version | conda-forge build | Licence declared by conda-forge | Source and recipe |
|---|---|---|---|---|
| cairo | 1.18.6 | `h477c42c_0` | LGPL-2.1-only or MPL-1.1 | [`packages/cairo-1.18.6-h477c42c_0`](../../../packages/cairo-1.18.6-h477c42c_0) |
| ffmpeg | 9.0.2 | `lgpl_hf2461e7_5` | LGPL-2.1-or-later | [`packages/ffmpeg-9.0.2-lgpl_hf2461e7_5`](../../../packages/ffmpeg-9.0.2-lgpl_hf2461e7_5) |
| fribidi | 1.0.18 | `hfd05255_0` | LGPL-2.1-or-later | [`packages/fribidi-1.0.18-hfd05255_0`](../../../packages/fribidi-1.0.18-hfd05255_0) |
| gdk-pixbuf | 2.44.8 | `h1f5b9c4_2` | LGPL-2.1-or-later | [`packages/gdk-pixbuf-2.44.8-h1f5b9c4_2`](../../../packages/gdk-pixbuf-2.44.8-h1f5b9c4_2) |
| graphite2 | 1.3.15 | `h5112557_1` | LGPL-2.0-or-later | [`packages/graphite2-1.3.15-h5112557_1`](../../../packages/graphite2-1.3.15-h5112557_1) |
| lame | 4.0 | `h0c5f640_1` | LGPL-2.0-only | [`packages/lame-4.0-h0c5f640_1`](../../../packages/lame-4.0-h0c5f640_1) |
| libglib | 2.90.1 | `ha564072_1` | LGPL-2.1-or-later | [`packages/libglib-2.90.1-ha564072_1`](../../../packages/libglib-2.90.1-ha564072_1) |
| libiconv | 1.18 | `hc1393d2_3` | LGPL-2.1-only | [`packages/libiconv-1.18-hc1393d2_3`](../../../packages/libiconv-1.18-hc1393d2_3) |
| libintl | 0.22.5 | `h5728263_4` | LGPL-2.1-or-later | [`packages/libintl-0.22.5-h5728263_4`](../../../packages/libintl-0.22.5-h5728263_4) |
| libpango | 1.58.2 | `h02b4fad_3` | LGPL-2.1-or-later | [`packages/libpango-1.58.2-h02b4fad_3`](../../../packages/libpango-1.58.2-h02b4fad_3) |
| librsvg | 2.62.4 | `h5506a08_0` | LGPL-2.1-or-later | [`packages/librsvg-2.62.4-h5506a08_0`](../../../packages/librsvg-2.62.4-h5506a08_0) |
| mpg123 | 1.33.7 | `ha58212f_1` | LGPL-2.1-only | [`packages/mpg123-1.33.7-ha58212f_1`](../../../packages/mpg123-1.33.7-ha58212f_1) |

The FFmpeg libraries are built `--disable-gpl --enable-version3` and report "LGPL version 3
or later" in their own binaries (`ffmpeg -L`); that, not conda-forge's metadata, is their licence.

The binaries each component contributes to the pack, and the conda-forge feedstock commit
each was built from, are listed in `index.json`.
