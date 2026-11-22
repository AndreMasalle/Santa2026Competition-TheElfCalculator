# Santa 2026 - The Elf Calculator

Solution for the Kaggle competition **Santa 2026 (The Elf Calculator)**: write the shortest possible arithmetic programs for 1,000 puzzles.

## Problem

Each puzzle provides:

- `starting_values`: a few small positive integers, loaded into registers 0, 1, 2, ... at the start
- `targets`: a list of integers that must appear at least once in some register
- `value_limit`: the largest value allowed in any register (intermediate values included)
- `registers`: 48 registers (indices 0-47)

An instruction has the form `["op", i, j, d]`: read registers `i` and `j`, apply `+`, `-`, `*`, or `/`, and write the result to register `d`.

**Score = total number of instructions across all 1,000 programs. Lower is better.**

### Rules

- All values must be positive integers.
- `-` is legal only if the first operand is greater than the second.
- `/` must be exact (no remainder).
- Results must not exceed `value_limit`.
- Source registers must already be defined.
- A target only needs to appear once, and it stays covered even if its register is overwritten later.
- A single invalid program causes the entire submission to be rejected.

Limits: at most 4,096 instructions per program and 128 KiB per CSV cell.

## Data files

| File | Contents |
|------|----------|
| `puzzles.csv` | The 1,000 scored puzzles (`scored_0001` - `scored_1000`) |
| `practice_puzzles.csv` | 200 practice puzzles, plus the columns `family`, `design_tier`, `lower_bound` |
| `sample_submission.csv` | A valid baseline for every puzzle |

The `starting_values` and `targets` columns are stored as JSON strings, so they need `json.loads` after being read with pandas.

## Santa Calculator

`santa_calculator` runs a program step by step, checks every rule above, and returns `(valid, instruction_count, message)`. `score_submission` runs it over an entire submission and sums the instruction counts. Always run it before uploading a submission.

## Progress

| Date | Notes | Score |
|------|-------|-------|
| 2026-11-22 | Baseline `sample_submission.csv` (about 1,490 instructions per puzzle on average) | 1,490,379 |  