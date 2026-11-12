# LP Review Agent: Goal and Checklist

## Goal

Give the agent one landing page URL. It reviews the page the way a real visitor experiences it, on phone and desktop, and reports everything that is slow, broken, wrong, inconsistent or confusing, ranked by how much it would hurt a visitor.

**In scope:** anything a visitor can see, read, tap or wait for.
**Out of scope:** the code behind the page, tracking and analytics, SEO internals, server setup, and comparing the page to ads.

## How it runs

- **Input:** one page URL, on demand.
- **Devices tested:** iPhone, Android phone, tablet and desktop.
- **Output:**
  - a short summary in chat
  - a full HTML report file with pass, warning or fail for each check, a screenshot and a plain-language fix for every problem, and fails listed first, ranked by how much they hurt a visitor
- **Safety:** the agent never submits forms. It only tests them up to the submit button.

## What gets checked

### 1. Speed: does it load fast?

Targets are Google's "good" thresholds unless noted.

| Check | Pass | Warning | Fail |
|---|---|---|---|
| Speed score (mobile and desktop) | 90+ | 50–89 | under 50 |
| Main content appears (LCP) | 2.5s or less | 2.5–4s | over 4s |
| Layout jumping while loading (CLS) | 0.1 or less | 0.1–0.25 | over 0.25 |
| Response to a tap (INP) | 200ms or less | 200–500ms | over 500ms |
| Total page size* | under 2 MB | 2–4 MB | over 4 MB |
| Oversized images* | none | any image over 200 KB | any image over 1 MB |
| Load on a slow phone connection* | fully usable within 5s | 5–10s | over 10s |

*Our own targets. Google has no standard for these.

### 2. First impression: what you see before scrolling

- On a phone, the headline, the main message and the call-to-action button are visible right away.
- It's clear within a few seconds what the page is offering.
- No popup or banner blocks the page right away.

### 3. Layout: does it look right on every screen?

- No sideways scrolling, overlapping elements, cut-off text or broken images.
- Sticky bars or chat bubbles don't cover buttons or form fields.
- Spacing, fonts and colors are consistent throughout.
- Images are sharp, not blurry or stretched.

### 4. Copy: is the writing correct?

- Spelling, grammar and punctuation.
- No leftover placeholder text, such as "lorem ipsum" or `{{token}}`.
- No dates or offers that have already expired.

### 5. Consistency: does the page agree with itself?

- The phone number, business name, offer, prices and dates are the same everywhere they appear.
- Buttons use matching wording and style.
- Headings follow the same capitalization rules.
- The tone stays the same from section to section.

### 6. Function: does everything work?

- Every link and button goes to a real page (no 404s or errors).
- Tapping the phone number dials the right number.
- Form (tested without submitting):
  - fields are easy to tap on a phone
  - the right keyboard appears for each field (number pad for phone, email keyboard for email)
  - required fields are marked
  - error messages are clear
- Videos play, sliders and tabs work, and in-page links scroll to the right spot.

### 7. Trust: would a stranger trust this page?

- Reviews or testimonials, a real address or contact information, and a privacy policy link.
- The padlock shows (HTTPS) and there are no security warnings.
- The browser tab title, the small icon in the tab and the preview image when the link is shared all look right.

### 8. Readability and accessibility

| Check | Pass | Fail |
|---|---|---|
| Body text size on a phone | 16px or larger (warning at 12–15px) | under 12px |
| Text contrast | 4.5:1 for normal text, 3:1 for large text | below that |
| Tap target size | 48×48px or larger (warning at 24–47px) | under 24px |
| Image descriptions (alt text) | present on all meaningful images | missing |
