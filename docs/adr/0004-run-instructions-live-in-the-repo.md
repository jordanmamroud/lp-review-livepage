# 0004: Everything a run uses lives in the repo, as plain files

**Status:** Accepted on 2026-11-12. One part is being re-tested: how a run gets these files (whether it copies the repo). See "Being tried" below.

## Context

A scheduled task has a saved prompt, and each run copies the repo (from the docs, not yet tested). The run's instructions could live in:
- **The scheduled task's saved prompt.** That isn't version-controlled.
- **A skill** in the repo, under `.claude/skills/` (Claude's suggestion, brainstorm Turn 8).
- **Plain files in the repo.**

Any Claude Code session in the repo reads `CLAUDE.md` automatically, including a scheduled run (from the docs, not yet tested). So a run sees the notes for working on the project whether it needs them or not.

## Decision

Jordan decided:

- **Everything a run uses lives in this repo, with version control, in one place** (Turn 5). The scheduled task's saved prompt is only a short pointer to the repo.
- **The run steps are a plain file, not a skill** (Turn 9, approved in Turn 13).
- **The files a run uses go in `src/`** (Turn 11, approved in Turn 13): the run steps (`src/scheduled-task.md`), the checklist (`src/checklist.md`) and the result format (`src/result-format.md`, its own file per Turn 19).
- **`CLAUDE.md` stays at the top level, for working on the project.** Its first line tells a run to follow `src/scheduled-task.md` (Turn 12, approved in Turn 13).

## Consequences

- Changing how reviews work means committing to the repo. The next run uses the latest version.
- The saved prompt's exact wording should be recorded in the repo once the scheduled task exists (checkpoint 1, issue #2).
- If the review ever needs to be run by name from other places, it could become a skill later.

## Being tried (not decided)

Jordan wants scheduled runs to load their instructions from GitHub without copying the whole repo. On 2026-11-12, a test tried a run with no repo attached. Its saved prompt pointed to one file in this repo, which the run read through the GitHub connector. Results: [issue #2 comment](https://github.com/jordanmamroud/lp-review-livepage/issues/2#issuecomment-6824961758). The `steps.md` named there is now `tests/connector-pattern/run-instructions.md`.

- **Worked:** no repo copied, reading files through the GitHub connector, saving a text file to Drive, no approvals needed.
- **Not tested yet:** passing the URL and job ID through the real API trigger, uploading images to Drive, and running browsers without a repo.

If runs end up working this way, part of this ADR changes. A run wouldn't copy the repo, so it wouldn't read `CLAUDE.md` automatically. The saved prompt would point straight to `src/scheduled-task.md`, and the first line of `CLAUDE.md` would no longer be how a run finds its steps. That change goes in a new ADR that replaces this one.

Either way, the rest stays: the files live in this repo, as plain files, in `src/`.
