# Test: can a run with no repo read GitHub and save to Drive? (throwaway)

You are a test run. The goal is to find out whether a scheduled run with no repository attached can follow instructions it reads from GitHub, and save a result to Google Drive with nobody approving anything. Do only these steps.

1. Run `pwd`, `ls -la` and `git rev-parse --show-toplevel 2>&1` in the shell. Note whether any repository was cloned into the session.
2. Read `tests/drive-and-github-access/code-word.md` from the GitHub repo `jordanmamroud/lp-review-livepage` through the GitHub connector. It contains a code word.
3. From the message sent with this run, take the `url` and `job_id`.
4. Create a plain text file in the Google Drive folder with ID `1vIME3xZJnvK0-47zATr7Wl2o1OCBxejF`, named `pattern-test_<job_id>.txt`. Put in it:
   - the code word from step 2,
   - the url and job_id from step 3,
   - a one-line summary of step 1 (was a repo cloned, and what was the working folder),
   - which tools you used to read GitHub and to write to Drive,
   - whether anything asked for approval or was blocked.
5. Do nothing else. Don't change the repo.
