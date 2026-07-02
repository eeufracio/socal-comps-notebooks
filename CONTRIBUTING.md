# Contributing / Workflow

This repo is a proprietary tool for Foremost Commercial Real Estate (see `LICENSE`), but it follows
standard git hygiene so it's easy to track changes, review them, and collaborate if others join in.

## Issues

Every non-trivial change starts as a GitHub Issue — bug or feature — using the templates under
`.github/ISSUE_TEMPLATE/`. Even a one-line issue is enough; the goal is a paper trail linking commits
to a reason.

## Branches

- `main` is always stable. Nothing is committed to it directly — everything lands via a merged PR.
- One branch per issue, cut from the latest `main`:

  ```bash
  git checkout main
  git pull
  git checkout -b <issue-number>-short-description
  ```

  e.g. `2-add-firm-city-to-competitive-landscape`.
- Keep branches scoped to one issue. Don't stack unrelated changes onto an existing branch — cut a
  new one off the updated `main` instead.

## Commits

- Summary line: short, imperative, under ~70 chars.
- Body: what changed and why — especially any judgment calls, edge cases found, or bugs caught
  along the way.
- Footer: `Fixes #N` / `Closes #N` so merging into `main` auto-closes the issue.

## Testing before opening a PR

The notebook has no automated test suite, so verify manually before committing:

1. Confirm every code cell still compiles (`compile(source, ..., "exec")` per cell, or just run the
   notebook top to bottom).
2. Exercise the changed function(s) directly against a real (or representative) CoStar export —
   don't rely on reading the code alone.
3. Check edge cases relevant to the change (blank fields, multi-office firms, unusual Property Type
   strings, etc.).

Never commit real CoStar exports, ledgers, or scorecards — they contain broker contact info and are
excluded via `.gitignore`. Use your own local copies for testing.

## Pull requests

Open a PR from your branch into `main` using `PULL_REQUEST_TEMPLATE.md`. Once merged, delete the
branch — start the next issue from a fresh branch off the updated `main`.
