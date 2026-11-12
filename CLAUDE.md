# lp-review-livepage instructions

**If you were started by a scheduled task or an API call to review a page, follow `src/run-instructions.md`. The rest of this file is for working on the project.**

The goal is to have an agent that reviews a live landing page so thoroughly that if it finds nothing wrong, I can be confident a real visitor won't run into any problems.

It looks at the page the way a real person would, on their phone or computer. Is it fast? Does it look right? Is the writing correct and consistent? Does every link, button and form work? Is there anything confusing or untrustworthy?

It only cares about what visitors actually see and experience, not the code behind the page.

The bar is simple: if a visitor would notice it, the agent should catch it first. A clean review should mean the page is ready. It shouldn't mean "probably fine."

## Scope

This repo only reviews pages and saves the result. Fixing pages, and the fix → re-review loop, are out of scope. A fixer, such as Jordan's km-lp-edit-page skill, would call this review.

## Working on the project

- The spec is GitHub issue #1. Work is broken into its sub-issues, one checkpoint at a time.
- Jordan's decisions between real alternatives go in `docs/adr/`, with related decisions grouped into one ADR. Drafts and open questions stay in the spec and the files. Follow the ADRs; if a decision changes, replace it with a new ADR.
- Every commit mentions the issue it's for with "Refs #N" (for example "Refs #2"). Don't use "Fixes #N", because that closes the issue on commit. An issue is closed only after a different agent acting as Jordan has checked it.
- Follow `MEMORY.md` (lessons learned in this repo). Log progress in `progress.md`, newest at the top.

## Files

- `src/run-instructions.md`: what a review run reads and does.
- `src/checklist.md`: everything a run checks.
- `src/result-format.md`: what a run saves, for agents and for people.
- `tests/<what-it-tests>/run-instructions.md`: what a test run reads and does. The folder name says what the test checks.
- `docs/adr/`: decisions and why they were made.
