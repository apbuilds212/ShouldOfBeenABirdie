# Should of Been a Birdie

A lightweight, mobile-first golf scorekeeping web app built for a single-day outing — "Tommy Gunz's 50th." It runs entirely in the browser from one self-contained `index.html` file, with no sign-up and no build step, so anyone in the group can open the link on their phone and start keeping score immediately. Scores can optionally sync **live** across every phone via Firebase, or work fully offline on a single device.

## What it does

The outing is a shotgun-start best-ball scramble across an 18-hole course (Douglaston Park, par 67). Twenty-four players are pre-loaded into six foursomes with staggered tee times. Each group's designated scorekeeper records the group's best-ball score hole-by-hole; the app labels every result (hole-in-one, eagle, birdie, par, bogey, double, and beyond), tracks the running total relative to par, and ranks all six groups on a shared leaderboard.

## Tabs

- **Welcome** — The intro note for the day, plus a one-tap "Play Tommy's Welcome" audio clip.
- **Tee Times** — The tee sheet: all six groups, their players, and start times.
- **Score** — Best-ball entry hole-by-hole with tap-friendly +/− steppers, par and yardage per hole, and live "to par" totals for the front nine, back nine, and full round. A **Scorekeeper Mode** toggle (PIN-gated) makes a phone the group's official scorekeeper; everyone else's Score tab is view-only and updates live.
- **Leaders** — The Master Leaderboard, ranked by score to par (lowest wins). Every row shows "kept by [name]" for transparency, and a group's final card can also be added manually by total strokes.
- **Sounds** — A soundboard of the celebration clips and trash-talk cues.

## Live shared leaderboard

When a Firebase Realtime Database is configured, the app runs in **Live** mode: each group's scorekeeper writes their group's card and every phone sees the leaderboard update within a second (the header shows a ● Live badge). Writes are guarded so a phone with a partial or empty card can never overwrite a group's fuller record — any holes it is missing are backfilled from the shared board rather than wiped. With no Firebase configured or no connection, the app falls back automatically to local, on-device scoring — nothing breaks. See `SETUP-Live-Leaderboard.md` for the ~12-minute setup.

## Features at a glance

- Best-ball, hole-by-hole entry with automatic result labeling and live to-par totals
- Shared live leaderboard with per-group scorekeeper attribution, plus manual total entry
- Multiple tee options, each with its own yardages and rating/slope
- Celebration sounds and voice clips for notable results, with a one-tap mute — audio lives in `audio/`
- Saved progress in the browser's `localStorage` (survives refreshes and accidental closes)
- Installable, full-screen web-app feel when added to a phone's home screen

## Running it

Everything is contained in `index.html`, so you can open that file in any modern browser or host it on any static host. A live version is published via **GitHub Pages**. To turn on the shared live board, follow `SETUP-Live-Leaderboard.md`.

## Tech

Plain HTML, CSS, and vanilla JavaScript — no frameworks, no build step. Firebase Realtime Database (optional) powers live sync; the Web Audio API drives tones, with pre-recorded voice clips layered on top for the reactions.

