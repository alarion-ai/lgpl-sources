# opencode 1.19.0: LGPL corresponding source

The Alarion `opencode` pack, version `1.19.0` (sha256
`eee184d04eafd3abca60e14c5a07ce9e9847f5aeebf17bc39eab5919a2dfeb15`), is the unmodified
`opencode-darwin-arm64` release binary of [opencode](https://github.com/anomalyco/opencode/releases/tag/v1.19.0) (MIT). That
binary embeds the Bun runtime, which statically links JavaScriptCore and WTF from Bun's fork of
WebKit, licensed under the GNU Lesser General Public License, version 2.

| Component | Exact version | Source |
|---|---|---|
| Bun | v1.3.14 (tag commit `0d9b296af33f2b851fcbf4df3e9ec89751734ba4`) | https://github.com/oven-sh/bun/tree/bun-v1.3.14 |
| WebKit / JavaScriptCore (LGPL-2) | commit `5488984d20e0dbfe4be2c3ba8fb18eb81a5e0e8b` | https://github.com/oven-sh/WebKit/tree/5488984d20e0dbfe4be2c3ba8fb18eb81a5e0e8b |

How these were identified, from the shipped binary: it reports `Bun v1.3.14`, and its embedded
header paths name `webkit-5488984d20e0dbfe-arm64`. Bun v1.3.14 pins that commit as
`WEBKIT_VERSION` in
[`scripts/build/deps/webkit.ts`](https://github.com/oven-sh/bun/blob/bun-v1.3.14/scripts/build/deps/webkit.ts),
and its prebuilt WebKit for that commit is
[`autobuild-5488984d20e0dbfe4be2c3ba8fb18eb81a5e0e8b`](https://github.com/oven-sh/WebKit/releases/tag/autobuild-5488984d20e0dbfe4be2c3ba8fb18eb81a5e0e8b).
The scripts that build it are in the Bun repository at that tag.

Alarion did not modify these components. The WebKit source is too large (~13 GB of history) to
copy here, so this index links the exact commits in their upstream repositories; if they become
unavailable, Alarion remains responsible for providing them — open an issue in this repository.
