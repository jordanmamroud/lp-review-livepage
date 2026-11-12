## 2026-11-12 07:52 CT · #2 Checkpoint 1: an unattended run saves a result to Drive
Where things stand (first entry; earlier work is in the issues and git history):
- The spec is issue #1. Its first checkpoint is issue #2. Decisions so far are in docs/adr/0001-0004.
- First test for #2 passed on Nov 12: a scheduled task with no repo attached read its instructions from this repo through the GitHub connector, followed them, and saved a text file to the Drive folder. Nothing asked for approval, and the run took about 35 seconds. Full results are in the comment on issue #2. That comment calls the test's file steps.md; it's now tests/connector-pattern/run-instructions.md.
- That test could not pass a URL and job ID into the run, because the test tool doesn't send them.
- Also on Nov 12, the repo switched to one task per agent, one commit per task, with this file as the status (see CLAUDE.md).

Next (all part of #2, one task at a time):
1. Pass url and job_id through the real API trigger, and confirm the run receives them. Check: the run's saved file shows both values.
   Not known yet: how to set up the API trigger and its token, and whether that needs Jordan in the claude.ai interface (#2, "To figure out"). Find that out first. If it needs him, ask him for that one step; don't skip the task.
2. Upload an image (not text) to Drive in an unattended run. Check: the image opens from Drive.
3. Get browsers (Playwright with Chromium and WebKit) working in a run with no repo, through the environment's setup script. Check: phone and desktop screenshots of landing.kitchenmagic.com/jm-test-page show the real page.
Then: the remaining acceptance criteria in #2, checked by a different agent acting as Jordan.

Open (not decided):
- Jordan wants one consistent pattern for how all his scheduled tasks load their instructions from GitHub (not a copy of the whole repo). The connector test above is the current candidate, and this project is where it's being worked out.
- Runs with no repo vs. a cloned repo: ADR 0004 and #2's first acceptance criterion still assume each run clones the repo and reads CLAUDE.md. If Jordan picks the connector way, both need updating (a new ADR, per CLAUDE.md). Until then, don't build the real task either way without asking him.
- What's still open in the spec: the browser and speed tools, the checklist's contents and thresholds, the JSON fields, and keeping the same issue id on a re-run.

Learned: -
Chat: https://claude.ai/code/session_01DTT9VFB7vFbN9G7guHKuUq (spec, connector test, and the switch to this workflow)

