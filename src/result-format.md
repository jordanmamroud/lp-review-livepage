# Result format

What a run hands back. It has two parts with the same content:

1. **Structured result (JSON):** for an agent that will act on it, for example to fix an issue.
2. **Full HTML report:** for a person to read.

## Structured result

A real-shaped example (the numbers and links are made up):

```json
{
  "page": "https://landing.kitchenmagic.com/jm-refacing-ppc",
  "reviewed_at": "2026-11-12T07:45:00Z",
  "verdict": "not ready",
  "could_not_check": [
    "Thank-you page after the form is submitted (forms are never submitted)",
    "Real iPhone Safari (WebKit was used as a stand-in)"
  ],
  "report_html": "https://.../report.html",
  "issues": [
    {
      "id": "phone-number-mismatch-footer",
      "level": "Blocker",
      "problem": "Footer phone number differs from the header and call button",
      "where": {
        "page": "https://landing.kitchenmagic.com/jm-refacing-ppc?gclid=test",
        "device": "iPhone 15, Safari, upright",
        "section": "Footer",
        "element": "footer a[href^='tel:']",
        "visible_text": "(610) 555-0193"
      },
      "evidence": {
        "found": "(610) 555-0193",
        "expected": "(610) 555-0139, as in the header and call button",
        "screenshot": "https://.../phone-number-mismatch-footer.png"
      },
      "how_to_see_it": "Open the page on a phone, scroll to the footer",
      "suggested_fix": "Change the footer number to (610) 555-0139",
      "how_to_confirm": "Re-run the consistency check: every phone number on the page matches"
    }
  ]
}
```

### What each field is for

- **page, reviewed_at:** what was reviewed and when. If the page changed since, the issues may be out of date.
- **verdict:** `ready`, `ready with minor fixes` or `not ready`.
- **could_not_check:** every blind spot. Never leave this out, even when it's empty.
- **report_html:** link to the full HTML report.
- **id:** a short descriptive name in lowercase with dashes, saying what and where. Lets an agent say "fixed phone-number-mismatch-footer". Being tried: giving the same problem the same id on a re-run, so a re-run shows whether it's gone.
- **level:** Blocker, Major or Minor (defined in `src/checklist.md`).
- **where:** the exact link (with any ad tracking used), device, browser and orientation, the section, and the visible text. **element** points at the spot in the page code, for the fixer. Leave it out when no single element is at fault, such as overall page speed.
- **evidence:** what was found versus what was expected. For speed and size checks, the measured number against the target (for example "4.8s" against "2.5s or less"). **screenshot** is a link to a separate image file, so an agent can open it.
- **how_to_see_it:** steps to see the problem again.
- **suggested_fix:** a plain-language fix.
- **how_to_confirm:** how to prove it's fixed.

## HTML report

The same content, for a person:

1. Verdict at the top.
2. What couldn't be checked.
3. Each issue, most serious first, with its screenshot and fix.
4. Every check that passed.

## Still open

- Where screenshots and the HTML report are stored, so their links work. This depends on how the result gets back to the caller (see `src/scheduled-task.md`).
