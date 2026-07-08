# Moving "Should of Been A Birdie" to your other Claude account

This folder contains everything for Tommy Gunz's 50th birthday golf app. To set it up under a different Claude account:

## Steps

1. **Save this whole folder** somewhere you can find it (it's already at `~/Downloads/Should of Been A Birdie`). If you're moving to a different computer, copy the entire folder — including the `deploy/` and `audio/` subfolders — to that machine.

2. **Switch accounts** in the Claude desktop app: sign out, then sign in with the other account (or use the account switcher if your version has one).

3. **Create a new project** in Cowork on that account. Name it whatever you like (e.g. "Should of Been A Birdie").

4. **Point the project at this folder** — select `Should of Been A Birdie` as the project's working folder so all the files below come along.

5. **Re-paste the project instructions** (these don't transfer between accounts):

   > Leverage this project space to create an application for Tommy Gunz's 50th birthday golf outing. I want the app to keep score, keep everyone honest, and have a great time.

That's it — the files do the heavy lifting; the account just needs the folder + instructions.

## What's in this package

- `deploy/index.html` — the live golf scoring app (open in a browser to run it)
- `deploy/audio/` — all the sound clips the app plays (birdie, eagle, "should've been a birdie", etc.)
- `50thBirthday - GOLF.csv` — the 24-golfer roster, tee groups, and tee times
- `Douglaston Scorecard - GolfNYC.html` — the course scorecard
- `Course Info.html` — Douglaston course details
- `SETUP-Live-Leaderboard.md` — notes on running the live leaderboard

## What does NOT carry over between accounts

Chat history, the project instructions (see step 5), and any connectors or memory tied to the original account. The files and the app itself are fully portable.
