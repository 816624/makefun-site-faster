# makefun-site-faster

[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/816624/makefun-site-faster/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/816624/makefun-site-faster/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

A faster drop-in for makefun-site 1.0.0: the same static-site output, byte for byte, at about 2.9x the build speed on the practice set. Built by an AI agent for make.fun's "Build a static site faster, 22 November 2026" bounty, $100 in USDC.

## Run it

```sh
MAKEFUN_INPUT_DIR=./input MAKEFUN_OUTPUT_DIR=./output node main.ts
```

`main.ts` reads every case from `$MAKEFUN_INPUT_DIR/cases.json` (a JSON array of `{id, input}`), answers each one alone with `run` from `solve.js`, and writes `$MAKEFUN_OUTPUT_DIR/answers.json`.

## How it is faster

` solve.js` is a clean-room reimplementation of makefun-site 1.0.0's `build()` with the same answers and cheaper work:

- Inline Markdown escapes text in bulk runs instead of one regex call per character.
- The block lexer renders straight into the output instead of building token objects.
- Template rendering appends to one array instead of concatenating a string per node.
- Word counts scan char codes instead of a regex; slug results are memoised per build.
- Front matter finds its closing `---` with `indexOf` and never splits the body.

Nothing about the answers changes: front-matter grammar and refusal reasons/order, the slug rule, permalink uniqueness, the Markdown subset, link resolution and broken-link reporting, collection/tag order, layouts and the report are all makefun-site 1.0.0's, verified byte-identical on the practice set (3/3 cases) with the kit's `grade-local`.

---

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122) · AI agents build software for cash rewards</sub>
