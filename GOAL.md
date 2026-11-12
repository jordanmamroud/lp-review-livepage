# LP Review Agent: What Gets Checked

The goal (from `CLAUDE.md`): if a visitor would notice it, the agent catches it first. A clean review means the page is ready.

This checklist is the **minimum**, not the limit. The agent must also do a free "fresh eyes" walk-through as a real visitor and report anything else that feels off, even if no check below covers it.

## How it runs

- **Input:** one live page URL, on demand.
- **Visits the page as real visitors do:**
  - small phone (iPhone SE size), regular iPhone, large Android phone, tablet, laptop and large desktop
  - Safari (iPhone) and Chrome, since most phone visitors use one of these
  - phone held upright and sideways
  - arriving with ad tracking added to the link (for example `?gclid=...` or `?utm_source=...`), since that's how ad visitors arrive
- **Never submits forms.** It tests them up to the submit button only.
- **Output:**
  - a short summary in chat
  - a full HTML report file with every check, a screenshot of every problem and a plain-language fix

## How problems are ranked

| Level | Meaning | Example |
|---|---|---|
| **Blocker** | A visitor can't do what the page is for | Call button dials the wrong number, form field can't be typed in |
| **Major** | Hurts trust or makes visitors leave | Typo in the headline, offer expired, page takes 8 seconds |
| **Minor** | Polish a careful visitor would notice | Uneven spacing, one button styled differently |

## What the report must also say

- **What it could not check**, for example the thank-you page after submitting, or a video it couldn't play. A clean review must never hide a blind spot.
- **Overall verdict:** ready, ready with minor fixes, or not ready.

---

## The checklist

### 1. Does the page load at all?

- The link opens the right page with no error, warning page or endless loading.
- It works with and without `www`, and `http` sends visitors to `https`.
- It still works when ad tracking is added to the link.
- There are no long chains of redirects before the page appears.
- The browser back button takes the visitor back, not into a loop.

### 2. Speed: does it load fast?

Google's "good" thresholds unless noted.

| Check | Pass | Warning | Fail |
|---|---|---|---|
| Speed score (mobile and desktop) | 90+ | 50–89 | under 50 |
| Main content appears (LCP) | 2.5s or less | 2.5–4s | over 4s |
| Layout jumping while loading (CLS) | 0.1 or less | 0.1–0.25 | over 0.25 |
| Response to a tap (INP) | 200ms or less | 200–500ms | over 500ms |
| Total page size* | under 2 MB | 2–4 MB | over 4 MB |
| Largest single image* | under 200 KB | 200 KB–1 MB | over 1 MB |
| Usable on a slow phone connection* | within 5s | 5–10s | over 10s |

\*Our own targets. Google has no standard for these.

Also checks:
- No blank screen or flash of unstyled page while loading.
- Fonts load properly, with no switch to a plain fallback font.
- Chat widgets, review widgets and maps don't slow the page or pop in late and push content around.

### 3. First impression: what you see before scrolling

- On a phone, the headline, the main message and the call-to-action button are visible right away.
- It's clear within about 5 seconds what's offered and what to do next.
- Nothing blocks the page right away, such as a popup or a cookie banner covering the button.
- The main image is relevant and loads sharp.

### 4. Layout: does it look right everywhere?

On every device, browser and orientation listed above:
- No sideways scrolling, overlapping elements, cut-off text or broken images.
- Faces and key details in photos aren't cropped off.
- Sticky headers aren't too tall, and sticky bars or chat bubbles don't cover buttons, fields or text.
- Spacing, fonts and colors are consistent from section to section.
- No empty sections, repeated sections or leftover blank space.
- Images are sharp, not blurry, stretched or squashed.
- Single words aren't stranded alone on the last line of a headline.
- The page still looks right when the phone uses dark mode.
- Animations are smooth, and the page doesn't hijack scrolling.

### 5. Copy: is the writing correct?

- Spelling, grammar and punctuation.
- No garbled characters, such as `â€™` showing instead of an apostrophe.
- No leftover placeholder text, such as "lorem ipsum", `{{token}}` or "headline here".
- No expired offers, dates in the past, or an out-of-date copyright year.
- Urgency claims like "today only" or "ends Friday" are actually true.
- Offers have the required fine print, and the fine print matches the offer.
- It's easy to read: short paragraphs and no jargon.

### 6. Consistency: does the page agree with itself?

- The phone number, business name, offer, prices, percentages and dates are the same everywhere they appear.
- Phone numbers and prices are written the same way each time.
- The browser tab title and the share preview match the page's offer.
- Buttons use matching wording and style.
- Headings follow the same capitalization rules.
- The tone stays the same, and no claims contradict each other.

### 7. Function: does everything work?

**Links and buttons**
- Every link and button goes to a real, working page (no 404s or errors).
- Links that leave the page open where expected (same tab or new tab).
- In-page links scroll to the right spot without hiding it under a sticky header.
- Anything that looks clickable is clickable, and anything clickable looks clickable.
- Buttons react visibly when tapped.

**Phone and email**
- Tapping the phone number dials the right number.
- Email links open an email with the right address.

**Form (tested without submitting)**
- The form is easy to find, and the call-to-action buttons lead to it.
- Every field can be tapped and typed in on a phone.
- The right keyboard appears for each field (number pad for phone, email keyboard for email).
- Labels stay visible while typing, rather than disappearing placeholder text.
- Phone autofill works on name, email, phone and address.
- Required fields are marked, and dropdowns show the right options.
- Error messages are clear and appear next to the right field.
- Consent and privacy text is present and readable.
- The form isn't longer than it needs to be.

**Everything else**
- Videos play, don't autoplay with sound, and have a visible play button.
- Sliders, tabs, accordions and popups open, close and work by tap.
- Embedded maps, review widgets and chat load and work.
- No visible error messages or features silently broken by page errors.

### 8. Trust: would a stranger trust this page?

- Reviews or testimonials look real and current.
- There's a real address or contact information.
- There's a working privacy policy link.
- Links to social profiles work, if present.
- The padlock shows (HTTPS) with no security or "not secure" warnings.
- The tab title, the small icon in the tab and the preview image when the link is shared all look right.
- Nothing looks spammy or scammy, such as too many popups, fake-looking countdowns or broken badges.

### 9. Readability and accessibility

| Check | Pass | Warning | Fail |
|---|---|---|---|
| Body text size on a phone | 16px+ | 12–15px | under 12px |
| Text contrast | 4.5:1 normal text, 3:1 large text | — | below that |
| Tap target size | 48×48px+ | 24–47px | under 24px |

Also checks:
- Images that matter have short text descriptions (alt text).
- Visitors can pinch-zoom on a phone.
- The page can be used with a keyboard, with visible focus on the selected element.
- Text over images is readable.

### 10. Fresh eyes walk-through (always required)

The agent scrolls the whole page on a phone as a first-time visitor and answers:
- Was anything confusing, annoying or suspicious?
- Was there a moment I'd have left the page? Where and why?
- Did anything look broken, cheap or unfinished?
- Is it obvious what to do next at every point?

Anything found here gets reported, even if it isn't on the checklist.
