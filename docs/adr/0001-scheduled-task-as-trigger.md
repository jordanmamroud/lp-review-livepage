# 0001: Start reviews with a Claude scheduled task (API trigger)

**Status:** Accepted on 2026-11-12, pending one unattended test run (see Consequences, and issue #2).

## Context

Reviews are started by Jordan's own agents (his Claude chats, tasks and skills), not by outsiders, for now. Results are saved to Google Drive for now.

Two ways to start a run were considered:

- **Claude scheduled task with an API trigger.** Runs on Jordan's Claude plan. Has a daily run limit. It's a research preview, so its limits and API may change. Can save to Drive through his Google Drive connector. Network access is limited by default and must be opened for the landing page sites.
- **GitHub Actions running Claude Code.** Real browsers and open internet. Each run is paid through an Anthropic API key. Saving to Drive would need its own Google login set up.

A third option, Jordan's own server, was not pursued. In the brainstorm, Claude described it as the most work.

The facts about scheduled tasks come from research in the brainstorm chat (https://claude.ai/chat/eba197aa-ad79-46ba-aa11-e7159c87f954, Turns 4-6). They have not been tested in a real run yet.

## Decision

Use a Claude scheduled task with an API trigger. Jordan chose this in https://claude.ai/code/session_01DTT9VFB7vFbN9G7guHKuUq, picking Claude's recommendation. That recommendation was based on results going to Drive, which the scheduled task can reach through his Drive connector.

## Consequences

- Before building more, one unattended test run must show the scheduled task can:
  - reach the landing pages (and the outside files they load),
  - run the browsers the review needs,
  - save files to Drive with nobody there to approve.
- If it can't, the fallback is GitHub Actions, and this ADR gets replaced.
- Callers hold the trigger's secret token. That's fine while only Jordan's own agents call it. Make goes in front if outsiders are added later.
