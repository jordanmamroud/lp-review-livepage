# Lessons learned in this repo

Rules future work must follow. Each has why, the date, and where it came from.

**A test run's instructions file is named `run-instructions.md`, not something vague like `steps.md`.** The test's folder says which test.
Why: Nov 12, 2026. Jordan couldn't tell what `steps.md` was for. (Jordan, in chat)

**Change only what Jordan asked for.** When he asks to rename one file, don't rename others, move folders or update related files beyond fixing references to that file. Suggest further changes instead.
Why: Nov 12, 2026. Asked to rename the test's `steps.md`, Claude also renamed `src/scheduled-task.md`, the test folder and `extra.md`, and had to undo it. (Jordan, in chat)

**Keep checks general, not tied to issues already found. Don't hard-code a specific rule like "body text is 18px". For now, no list of each page's phone number (Jordan: "maybe later").** A check that's specific to how Kitchen Magic pages work, like the town text, is fine.
Why: Nov 13, 2026. A draft of the checks was built from the old km-landing-pages rules file, and Jordan said those rules were too specific to issues already found. He doesn't want to keep a list of each page's phone number for now. (Jordan, in chat)

**The form check is simple: use the form like a visitor would, pressing the buttons and typing through every step, to confirm it isn't broken, and never submit.** Don't add detailed cases like a zip code outside the service area.
Why: Nov 13, 2026. Jordan said a detailed list of form cases was more than he wanted. (Jordan, in chat)
