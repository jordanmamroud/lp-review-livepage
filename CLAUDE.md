# lp-review-livepage instructions

**If you were started by a scheduled task or an API call to review a page, follow `src/scheduled-task.md`. The rest of this file is for working on the project.**

The goal is to have an agent that reviews a live landing page so thoroughly that if it finds nothing wrong, I can be confident a real visitor won't run into any problems.

It looks at the page the way a real person would, on their phone or computer. Is it fast? Does it look right? Is the writing correct and consistent? Does every link, button and form work? Is there anything confusing or untrustworthy?

It only cares about what visitors actually see and experience, not the code behind the page.

The bar is simple: if a visitor would notice it, the agent should catch it first. A clean review should mean the page is ready. It shouldn't mean "probably fine."

## Scope

This repo only reviews pages and saves the result. Fixing pages, and the fix → re-review loop, are out of scope. A fixer, such as Jordan's km-lp-edit-page skill, would call this review.

## Working on the project

Work goes one task at a time (Matt Pocock's approach). Each task is done by an agent that starts fresh and knows only what's in this repo and its issues. So everything the next agent needs must be here.

1. **Catch up.** Read MEMORY.md, the top entry of `progress.md`, `git log --oneline -10`, and the open issues. The spec is issue #1. Checkpoints are its sub-issues.
2. **Pick one task.** Take the next step on the earliest open checkpoint that isn't blocked. Do only that task.
3. **Finish it.** Add a dated entry at the top of `progress.md` with what was done, what's next and what was learned. Results and findings go there too, not in issue comments. Then make **one commit for the whole task**, never one per file, and push it to `main`. The commit mentions its issue with "Refs #N" (for example "Refs #2"). Don't use "Fixes #N", because that closes the issue on commit.
4. **Closing.** An issue is closed only after a different agent acting as Jordan has checked it.

Decisions: Jordan's decisions between real alternatives go in `docs/adr/`, with related decisions grouped into one ADR. Drafts and open questions stay in the spec and the files. Follow the ADRs; if a decision changes, replace it with a new ADR.

## Files

- `src/scheduled-task.md`: the steps a run follows.
- `src/checklist.md`: everything a run checks.
- `src/result-format.md`: what a run saves, for agents and for people.
- `docs/adr/`: decisions and why they were made.
- `progress.md`: where the work stands, newest entry at the top.
- `MEMORY.md`: lessons from Jordan that change how work is done here.
- `tests/`: throwaway tests of how runs work, one folder per test.
