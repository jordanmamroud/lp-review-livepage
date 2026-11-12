# 0004: Everything a run uses lives in the repo, as plain files

**Status:** Accepted on 2026-11-12.

## Context

A scheduled task has a saved prompt, and each run copies the repo (from the docs, not yet tested). The run's instructions could live in different places:
- **In the scheduled task's saved prompt.** That isn't version-controlled.
- **As a skill** in the repo, under `.claude/skills/` (Claude's suggestion in brainstorm Turn 8).
- **As plain files in the repo.**

Any Claude Code session in the repo reads `CLAUDE.md` automatically, including a scheduled run (from the docs, not yet tested). So a run sees the notes for working on the project whether it needs them or not.

## Decision

Jordan decided:

- **Everything a run uses lives in this repo, with version control, in one place** (Turn 5). The scheduled task's saved prompt is only a short pointer to the repo.
- **The run steps are a plain file, not a skill** (Turn 9, approved in Turn 13).
- **The files a run uses go in `src/`** (Turn 11): the run steps (`src/scheduled-task.md`), the checklist (`src/checklist.md`) and the result format (`src/result-format.md`, its own file per Turn 19).
- **`CLAUDE.md` stays at the top level, for working on the project.** Its first line tells a run to follow `src/scheduled-task.md`.

## Consequences

- Changing how reviews work means committing to the repo. The next run uses the latest version.
- The saved prompt's exact wording should be recorded in the repo once the scheduled task exists (checkpoint 1, issue #2).
- If the review ever needs to be run by name from other places, it could become a skill later.
