# Fast makefun-site drop-in

[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/gregorionainggolan8-tech/makefun-site-generator-speed-01-run-20261122/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/gregorionainggolan8-tech/makefun-site-generator-speed-01-run-20261122/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

A faster drop-in for makefun-site 1.0.0 (`site-generator-speed-01-run-20261122`):
`solve.js` returns byte-for-byte the same output tree as makefun-site 1.0.0 for
every input, but faster.

## How it is faster

- Hand-written scanners replace the reference's per-line and per-character
  regular expressions (front matter, Markdown blocks, template tags).
- HTML escaping and inline Markdown rendering work on whole runs of plain
  text instead of escaping one character at a time.
- Slug results are cached within a single build (titles and tag names repeat).
- Template rendering writes into one shared output array instead of
  concatenating a string at every node.
- No network, no clock, no randomness; nothing is kept from one `run(input)`
  call to the next.

## Layout

- `solve.js` — dependency-free ES module, `run(input)` is the entrypoint.
- `main.ts` — the driver: reads `/input/cases.json` (or
  `MAKEFUN_INPUT_DIR`), answers each case with `run`, writes
  `/output/answers.json` (or `MAKEFUN_OUTPUT_DIR`).
- `package.json` — `{"type": "module"}`.
- `LICENSE` — MIT.

## Grade locally

From the unpacked kit directory (replace `<kit>` with its path):

```sh
node <kit>/cli/makefun.mjs grade-local --kit <kit> --bot <this directory> --driver docker
```

Or directly, without the kit:

```sh
MAKEFUN_INPUT_DIR=<kit>/practice/input MAKEFUN_OUTPUT_DIR=/tmp/out node main.ts
```

then compare `/tmp/out/answers.json` against
`<kit>/practice/reference/expected.json` (one answer per case, in order).

Built for the make.fun bounty [Build a static site faster, 22 November 2026](https://make.fun/bounty/site-generator-speed-01-run-20261122).
