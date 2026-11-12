# Result format

What a run saves. It has two parts describing the same review:

1. **Structured result (`result.json`):** for an agent that will act on it, for example to fix an issue.
2. **Full HTML report (`report.html`):** for a person to read. It also lists every check that passed.

Where they're saved is in `src/scheduled-task.md`. This format is a draft and may change as checkpoints are built (spec: issue #1).

## Structured result

A real-shaped example (the numbers and links are made up):

```json
{
  "job_id": "2026-11-12-0207_jm-refacing-ppc",
  "status": "done",
  "page": "https://landing.kitchenmagic.com/jm-refacing-ppc",
  "reviewed_at": "2026-11-12T02:07:00-06:00",
  "verdict": "not ready",
  "could_not_check": [
    "Thank-you page after the form is submitted (forms are never submitted)",
    "Real iPhone Safari (WebKit was used as a stand-in)"
  ],
  "report_html": "https://drive.google.com/file/d/.../view",
  "issues": [
    {
      "id": "phone-number-mismatch-footer",
      "level": "Blocker",
      "problem": "Footer phone number differs from the header and call button",
      "where": {
        "page": "https://landing.kitchenmagic.com/jm-refacing-ppc?gclid=test",
        "device": "iPhone 15 size, WebKit (Safari stand-in), upright",
        "section": "Footer",
        "element": "footer a[href^='tel:']",
        "visible_text": "(610) 555-0193"
      },
      "evidence": {
        "found": "(610) 555-0193",
        "expected": "(610) 555-0139, as in the header and call button",
        "screenshot": "https://drive.google.com/file/d/.../view"
      },
      "how_to_see_it": "Open the page on a phone, scroll to the footer",
      "suggested_fix": "Change the footer number to (610) 555-0139",
      "how_to_confirm": "Re-run the review: every phone number on the page matches"
    }
  ]
}
```

A failed run saves only what it can, for example:

```json
{
  "job_id": "2026-11-12-0207_jm-refacing-ppc",
  "status": "failed",
  "failure_reason": "The page didn't load: the network blocked landing.kitchenmagic.com",
  "page": "https://landing.kitchenmagic.com/jm-refacing-ppc",
  "reviewed_at": "2026-11-12T02:07:00-06:00"
}
```

### What each field is for

- **job_id:** the name of this review's folder in Google Drive.
- **status:** `done` or `failed`. Always present, so a caller never waits on a run that crashed.
- **failure_reason:** only when status is `failed`. What stopped the run, in plain words.
- **page, reviewed_at:** what was reviewed and when (Central time). If the page changed since, the issues may be out of date.
- **verdict:** `ready`, `ready with minor fixes` or `not ready`. Only in a `done` result.
- **could_not_check:** every blind spot. Never leave this out of a `done` result, even when it's empty.
- **report_html:** link to the full HTML report.
- **id:** a short descriptive name in lowercase with dashes, saying what and where. Lets an agent say "fixed phone-number-mismatch-footer". Being tried: giving the same problem the same id on a re-run, so a re-run shows whether it's gone.
- **level:** Blocker, Major or Minor (defined in `src/checklist.md`).
- **where:** the exact link (with any ad tracking used), device, browser and orientation, the section, and the visible text. **element** points at the spot in the page code, for the fixer. Leave it out when no single element is at fault, such as overall page speed.
- **evidence:** what was found versus what was expected. For speed and size checks, the measured number against the target (for example "4.8s" against "2.5s or less"). **screenshot** is a link to a separate image file in the job's `screenshots` folder, so an agent can open it.
- **how_to_see_it:** steps to see the problem again.
- **suggested_fix:** a plain-language fix.
- **how_to_confirm:** how to prove it's fixed.

## HTML report

The same review, for a person:

1. Verdict at the top.
2. What couldn't be checked.
3. Each issue, most serious first, with its screenshot and fix.
4. Every check that passed.
