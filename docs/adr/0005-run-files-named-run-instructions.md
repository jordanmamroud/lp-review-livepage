# 0005: Files a run follows are named run-instructions.md

**Status:** Accepted on 2026-11-12. Changes only the file name in ADR 0004.

## Context

ADR 0004 put the review run's steps in `src/scheduled-task.md`. The first test run used `tests/connector-pattern/steps.md`. Jordan found both names unclear: "steps" doesn't say whose steps or what for, and "scheduled-task" sounds like something on a timer, while reviews start from an API call.

## Decision

Jordan decided (https://claude.ai/code/session_01DTT9VC6zJWzQETbFhA1mKQ):

- **Any file a run reads and follows is named `run-instructions.md`.** The folder it's in says which run.
- The review run's file is `src/run-instructions.md`.
- Each test's file is `tests/<what-it-tests>/run-instructions.md`, with a folder name that says what the test checks. The first test is `tests/drive-and-github-access/`.

## Consequences

- Every reference to `src/scheduled-task.md` now points to `src/run-instructions.md`. ADR 0004 is left as written, with a note pointing here.
- A scheduled task's saved prompt must point to the new path. The test task's prompt was updated with this change.
