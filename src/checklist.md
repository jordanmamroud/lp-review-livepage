# LP Review Agent: What Gets Checked

The goal (from `CLAUDE.md`): if a visitor would notice it, the agent catches it first. A clean review means the page is ready.

This checklist is the **minimum**, not the limit. The agent must also do a free "fresh eyes" walk-through as a real visitor and report any other fault it finds, even if no check below covers it.

The checklist's contents and thresholds haven't been reviewed by Jordan yet (spec: issue #1).

## How it runs

- **Input:** one live page URL and a job ID, on demand (see `src/scheduled-task.md`).
- **Visits the page as real visitors do:**
  - small phone (iPhone SE size), regular iPhone, large Android phone, tablet, laptop and large desktop
  - Chrome, and Safari's engine (WebKit) as a stand-in for iPhone Safari, since most phone visitors use one of these. Real iPhone Safari is always listed under what couldn't be checked.
  - phone held upright and sideways
  - arriving with ad tracking added to the link (for example `?gclid=...` or `?utm_source=...`), since that's how ad visitors arrive
- **Never submits forms.** It tests them up to the submit button only.
- **Output:** a structured result for agents and a full HTML report for people, both described in `src/result-format.md`.

## What counts as a problem

The agent finds faults. It doesn't give advice.

- **Report it** if a visitor would be stopped, confused or put off by the page as it is.
- **Leave it out** if the sentence would start with "it would be better if".

Major design faults count. Small suggestions don't. A suggested fix for a reported fault is fine. Ideas for improving the page are not. For example:

- Report: a popup covers the main button. Leave out: the popup's headline could be friendlier.
- Report: text overlaps a photo on a phone. Leave out: more space between sections would look cleaner.
- Report: a paragraph is too small to read. Leave out: a different font would look more modern.

## How problems are ranked

| Level | Meaning | Example |
|---|---|---|
| **Blocker** | A visitor can't do what the page is for | Call button dials the wrong number, form field can't be typed in |
| **Major** | Hurts trust or makes visitors leave | Typo in the headline, offer expired, page takes 8 seconds |
| **Minor** | A small fault a careful visitor would notice | Typo in the small print, out-of-date copyright year |

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

Google's "good" thresholds unless noted. Tap speed (INP) is not checked: it can't be measured reliably in a single cloud run.

| Check | Pass | Warning | Fail |
|---|---|---|---|
| Speed score (mobile and desktop) | 90+ | 50–89 | under 50 |
| Main content appears (LCP) | 2.5s or less | 2.5–4s | over 4s |
| Layout jumping while loading (CLS) | 0.1 or less | 0.1–0.25 | over 0.25 |
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
- The main image loads, is sharp, and isn't clearly the wrong image for the offer.

### 4. Layout: does it look right everywhere?

On every device, browser and orientation listed above:
- No sideways scrolling, overlapping elements, cut-off text or broken images.
- Faces and key details in photos aren't cropped off.
- Sticky headers, sticky bars and chat bubbles don't cover buttons, fields or text.
- A sticky header doesn't take up so much of a phone screen that the page is hard to use.
- No spacing, font or color is clearly a mistake, such as one section in a different font.
- No empty sections, repeated sections or leftover blank space.
- Images are sharp, not blurry, stretched or squashed.
- Nothing breaks when the phone uses dark mode, such as text or a logo that can't be seen.
- Animations are smooth, and the page doesn't hijack scrolling.

### 5. Copy: is the writing correct?

- Spelling, grammar and punctuation.
- No garbled characters, such as `â€™` showing instead of an apostrophe.
- No leftover placeholder text, such as "lorem ipsum", `{{token}}` or "headline here".
- No expired offers, dates in the past, or an out-of-date copyright year.
- Urgency claims like "today only" or "ends Friday" are actually true.
- Offers have the required fine print, and the fine print matches the offer.

### 6. Consistency: does the page agree with itself?

- The phone number, business name, offer, prices, percentages and dates are the same everywhere they appear.
- The browser tab title and the share preview match the page's offer.
- No button looks like a mistake next to the others, such as one in a different color.
- No claims contradict each other.

### 7. Function: does everything work?

**Links and buttons**
- Every link and button goes to a real, working page (no 404s or errors).
- Links that leave the page open where expected (same tab or new tab).
- In-page links scroll to the right spot without hiding it under a sticky header.
- Anything that looks clickable is clickable, and anything clickable looks clickable.
- Buttons react visibly when tapped.

**Phone and email**
- Tapping a phone number dials the same number it shows.
- There are no hidden or empty phone links.
- Email links open an email with the right address.

**Form (used like a visitor, never submitted)**
- The form is easy to find, and the call-to-action buttons lead to it.
- The form is used like a visitor would, pressing the buttons and typing in the fields through every step, to confirm it isn't broken.
- It stops before the submit button.

**Town text (Kitchen Magic pages)**
- With a town code in the link (for example `?loc_id=1014679`, which is Bridgeport), the visitor's town shows.
- With no town code, the "Near You" wording shows.

**Everything else**
- Videos play, don't autoplay with sound, and have a visible play button.
- Sliders, tabs, accordions and popups open, close and work by tap.
- Embedded maps, review widgets and chat load and work.
- No visible error messages or features silently broken by page errors.

### 8. Trust: would a stranger trust this page?

- Reviews or testimonials aren't broken, empty or clearly out of date.
- There's a real address or contact information.
- There's a working privacy policy link.
- Links to social profiles work, if present.
- The padlock shows (HTTPS) with no security or "not secure" warnings.
- The tab title, the small icon in the tab and the preview image when the link is shared all look right.
- Nothing clearly looks spammy or scammy, such as a fake-looking countdown or a broken badge.

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
- Did anything look broken or unfinished?
- Is it obvious what to do next at every point?

Any fault found here gets reported, even if it isn't on the checklist. Ideas for making the page better are left out (see "What counts as a problem").
