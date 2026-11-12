# 0002: How a caller asks for a review and gets the result

**Status:** Accepted on 2026-11-12.

## Context

The goal from the start: something sends a landing page URL in an API call, and that starts a review (brainstorm Turn 3). Jordan also said the caller has to get the result back in a form it can act on, and email alone isn't enough, because the caller may be an agent (Turns 15, 17).

The scheduled-task API only starts a run and returns a session link. It has no "get the result" call. Claude said this in Turn 30; it wasn't checked against the docs or tested. A review takes minutes, so the caller can't just wait on the request.

Options discussed for getting the result back:
- **Callback:** the caller sends a "reply to" address, and the run posts the result there (Turns 16, 22, 24).
- **The caller checks a fixed place** for a result saved under a job ID (Turns 16, 30).
- **A storage event, or "watcher":** saving the result triggers whatever reacts next (Turn 28). This needs storage that supports events, such as Supabase.
- **Email:** fine for a person, but not for an agent.

Options discussed for who calls it:
- Only Jordan's own agents (his Claude chats, tasks and skills).
- Outsiders too, with a Make webhook in front to hide the trigger's token (Turns 4, 24).

Options for the input:
- The URL only (Turn 3).
- The URL plus a job ID that the run makes up if it's missing (what the repo said after Turn 36).
- The URL plus a required job ID.

## Decision

Jordan decided these in the grilling session (https://claude.ai/code/session_01DTT9VFB7vFbN9G7guHKuUq), except where a brainstorm turn is cited:

- **Only Jordan's own agents call it.** They hold the trigger's secret token. There is no Make in front.
- **The caller sends `url` and `job_id`. Both are required, and the caller makes the job ID** so it knows where to look.
- **The job ID is the job folder's name, and it starts with the date and time to the minute** (Jordan, brainstorm Turn 33). The rest of the format is a draft (see `src/scheduled-task.md`).
- **If the job ID is missing, the run stops and says so.** It never makes one up. If the URL is missing or invalid, it saves a failed result.
- **The caller checks the job's results folder for the result.**
- **The run always saves `result.json` with a status, `done` or `failed`,** plus the reason when it failed. This holds even when the run can't finish.
- **The caller gives up after about 30 minutes** if nothing appears, and tells Jordan.

## Consequences

- Callers need the trigger token and access to Jordan's Google Drive. That limits callers to his own agents, which is the intent for now.
- For now nothing is sent back to the caller directly. A callback or storage event could be added later without changing how the run saves results.
- Adding outsiders later means putting Make in front, and probably different storage. That would be a new ADR.
