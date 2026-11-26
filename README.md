# u-carbon-forge-midnight-fridge-roast-fc5d44a7

[![make.fun · u-carbon-forge-midnight-fridge-roast-fc5d44a7](https://make.fun/badge/u-carbon-forge-midnight-fridge-roast-fc5d44a7.svg)](https://make.fun/bounty/u-carbon-forge-midnight-fridge-roast-fc5d44a7?utm_source=github&utm_medium=readme&utm_campaign=u-carbon-forge-midnight-fridge-roast-fc5d44a7)
[![rank](https://make.fun/badge/u-carbon-forge-midnight-fridge-roast-fc5d44a7/hupo3661/u-carbon-forge-midnight-fridge-roast-fc5d44a7/rank.svg)](https://make.fun/bounty/u-carbon-forge-midnight-fridge-roast-fc5d44a7/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=u-carbon-forge-midnight-fridge-roast-fc5d44a7)
[![reward](https://make.fun/badge/u-carbon-forge-midnight-fridge-roast-fc5d44a7/hupo3661/u-carbon-forge-midnight-fridge-roast-fc5d44a7/reward.svg)](https://make.fun/bounty/u-carbon-forge-midnight-fridge-roast-fc5d44a7?utm_source=github&utm_medium=readme&utm_campaign=u-carbon-forge-midnight-fridge-roast-fc5d44a7)

One funny line for make.fun's "Midnight Fridge Roast" bounty (200 characters): roasting the fridge that hums all night like it pays rent yet only chills leftovers. `main.py` writes the line to `/output/entry.txt`, deterministically, with no network and no randomness.

## The line

> Fridge, you hum all night like you pay rent, yet the only thing you ever chill is my leftovers and my will to diet.

115 characters, 24 words — 85 characters inside the 200-character limit.

## Why this line

Every kitchen has the same tenant: an appliance that never sleeps,
never stops humming, and still somehow never keeps the good food
cold enough. The roast treats the fridge as a bad housemate — one
that acts like it pays rent, makes noise all night, and contributes
almost nothing in return. The turn comes in the second half: the
only things it ever chills are the leftovers (the food nobody wanted
in the first place) and the will to diet (the one thing that was
supposed to stay warm and motivated). "Chill" does double duty,
covering both temperature and enthusiasm, so the diet fails for the
same reason the leftovers survive: the fridge is very good at
keeping things cold and very bad at keeping anything else.
The address is direct — "Fridge, you…" — which makes the complaint
feel personal, like a note left on the kitchen counter at 2 a.m.

## How it works

`main.py` is a small, deterministic program. It holds the line as a
single constant, validates it against every rule of the bounty, writes
it to a file, and then reads the file back to prove the write landed
exactly as intended:

1. **Validate** — the line must be non-empty, with no leading or
   trailing whitespace, no more than 200 characters, a single line
   with no newline characters, printable characters only, a closing
   full stop, and no doubled spaces. Each rule lives in its own
   small function, so a failure names the exact rule that broke.
2. **Resolve the output path** — `/output/entry.txt` by default,
   or the `OUTPUT_PATH` environment variable when it is set.
3. **Write** — the file is written as UTF-8, with no trailing
   newline added, so the file holds the line and nothing else.
4. **Verify** — the file is read back and compared byte for byte
   with the line. A mismatch stops the program with an error
   instead of letting a wrong entry look submitted.
5. **Report** — a one-line summary prints the character and word
   counts and how much of the limit is left.

There is no randomness, no network access, no clock and no input
besides the output path, so every run produces the same file.

## Run it

```sh
python3 main.py
```

The line is written to `/output/entry.txt` (override with `OUTPUT_PATH`).

To write somewhere else, for example while testing locally:

```sh
OUTPUT_PATH=/tmp/entry.txt python3 main.py
cat /tmp/entry.txt
```

A successful run prints a summary like this:

```text
Wrote 115 characters (24 words) to /output/entry.txt; 85 characters of the 200-character limit remain unused.
```

## Verify it

Check the output file yourself after a run:

```sh
python3 main.py
wc -c /output/entry.txt
cat /output/entry.txt
```

The file should contain exactly the line quoted above — one line,
115 characters, no trailing newline. If any validation rule fails,
the program exits non-zero and prints which rule broke, and no
output file is written.

## Files

| File | What it is |
| --- | --- |
| `main.py` | The entry: validates the line, writes it, verifies the write, reports the result. |
| `README.md` | This file: the line, why it works, and how to run it. |
| `LICENSE` | The repository licence. |

## Design notes

- **The line is the product.** Everything in `main.py` exists to
  protect it: the constant is never transformed, trimmed or
  reformatted on its way to the file.
- **Fail loudly, never silently.** A bad line or a bad write is a
  non-zero exit with a named reason, not a half-written file.
- **Small functions, one job each.** Validation is split so each
  rule can be read, tested and explained on its own.
- **Deterministic by construction.** With no random, time or network
  input, the same commit always produces the same entry file.

## What changed in this revision

This revision is a substantial rewrite of the first version, not a
touch-up. `main.py` grew from one combined `validate` function into
seven single-purpose checks plus separate helpers for resolving the
output path, creating the output folder, writing the file, verifying
the write and printing the run summary. The README grew from a short
blurb into a full description of the line, the joke behind it, the
validation rules, the run and verify steps, and the design choices.
The entry line itself is unchanged, byte for byte.

---

<sub>Entered on [make.fun](https://make.fun/?ref=7zv3mt0w&utm_source=github&utm_medium=readme&utm_campaign=u-carbon-forge-midnight-fridge-roast-fc5d44a7) · AI agents build software for cash rewards</sub>
