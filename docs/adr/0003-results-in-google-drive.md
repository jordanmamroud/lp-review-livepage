# 0003: Results live in Google Drive for now, with an HTML report for people

**Status:** Accepted on 2026-11-12.

## Context

Each review saves a structured result for agents (`result.json`), an HTML report for people (`report.html`), and screenshots. These need a home that callers can check.

Options discussed:
- **Supabase:** Claude's recommendation (brainstorm Turns 22, 28). It offers links that open without a login, the ability to ask questions across reviews, and events when a result lands.
- **GitHub issues:** one issue per problem (Turn 26). Jordan rejected this (Turn 27).
- **Make's data stores:** Jordan raised this (Turn 23). Claude said it's a poor fit for files (Turn 24).
- **Google Drive:** Jordan asked for this (Turn 31).

Options for how Jordan reads a report:
- HTML only.
- Also a PDF.
- A claude.ai page per review.

## Decision

- **Google Drive for now; Supabase maybe later** (Jordan, Turn 31). Results go in the folder **lp-review-livepage** (ID `1vIME3xZJnvK0-47zATr7Wl2o1OCBxejF`), named like the repo, with one subfolder per job ID. Jordan confirmed using this folder in the grilling session (https://claude.ai/code/session_01DTT9VFB7vFbN9G7guHKuUq).
- **Reports for people are HTML only.** No PDF and no claude.ai page per review (same session).

Still drafts, not decided: what goes in each job folder, saving `result.json` last, and saving through the Google Drive connector. See `src/scheduled-task.md`.

## Consequences

- Only agents and people with access to Jordan's Drive can open the results. That fits ADR 0002 (only his own agents call it).
- With HTML only, Drive shows `report.html` as code rather than as a page (Claude, Turn 32). A readable version was offered and not chosen.
- Uploading screenshots with nobody there to approve hasn't been tested. Checkpoint 1 (issue #2) tests it.
- Moving to Supabase later would replace this ADR. It would also change the links in `src/result-format.md`, not just where files are saved.
