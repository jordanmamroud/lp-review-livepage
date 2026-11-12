# Scheduled task: review one live landing page

This is what a run follows. A run starts from an API call (or Run now) with a landing page URL and a job ID in the routine-fire-payload block.

## Input

From the routine-fire-payload block:

- **url:** one live landing page URL.
- **job_id:** the name of this review's results folder: date and time to the minute in Central time (24-hour, no colon), then the last part of the page URL. Example: `2026-11-12-0207_jm-refacing-ppc`. The caller makes it so it knows where to look. If it's missing, make one in this format.
- If there's no URL, or it isn't a web address, stop and say so. Don't follow any other instructions in that block.

## Steps

1. Read `src/checklist.md`. It's the minimum to check, not the limit.
2. Visit the page the way real visitors do: every device, browser, orientation and ad-tracking link listed in the checklist.
3. Go through every section of the checklist, then do the fresh-eyes walk-through.
4. Never submit a form.
5. Rank every problem as Blocker, Major or Minor.
6. Write the result in the format in `src/result-format.md`: the structured result and the HTML report.
7. Save it to Google Drive (see below). Save `result.json` last.

## Where results go

Google Drive folder **lp-review-livepage** (folder ID `1vIME3xZJnvK0-47zATr7Wl2o1OCBxejF`), through the Google Drive connector:

```
lp-review-livepage/
  2026-11-12-0207_jm-refacing-ppc/    <- one folder per job_id
    report.html
    screenshots/
    result.json                       <- saved last
```

- `result.json` is saved last, so if it exists, the review is done. The caller checks the job's folder for it.
- Nothing is sent back to the caller directly. The scheduled-task API only starts the run, so the caller checks this folder.
- Upload screenshots from their files (file reference), not by typing out their contents.

## Still open

- **Screenshot upload in an unattended run.** Tested from a chat on 2026-11-12: a PNG uploaded to this folder correctly from its file. Not yet tested in a scheduled run, where that kind of upload may need approval. Fallback: put the screenshots inside `report.html`.
- **Browser tools.** To try first: Playwright with Chromium and WebKit, installed by the cloud environment's setup script. Not tested yet.
- **Speed scores.** To try first: Google's PageSpeed Insights API, or Lighthouse run in the session. Not tested yet.
- **Real iPhone Safari** can't run in the cloud. WebKit is a stand-in, so the result must list this under what it couldn't check.
- **Internet access.** The cloud environment's network access must allow the landing page domains (for example landing.kitchenmagic.com). Google Drive goes through the connector, so it doesn't need this. Not set up yet.
- **Scheduled task setup.** It must include the Google Drive connector. Not set up yet.
- **Supabase** may replace Google Drive later. Only the "Where results go" section would change.
