# Should of Been a Birdie

A lightweight, mobile-first golf scorekeeping web app built for a single-day outing — "Tommy's 50th." It runs entirely in the browser as one self-contained `index.html` file, with no server, no sign-up, and no dependencies, so anyone in the group can open the link on their phone and start keeping score immediately.

## What it does

The app is designed for a shotgun-style group scramble across an 18-hole course (par 67). Players are pre-loaded into six groups, and each group records strokes hole-by-hole using simple plus/minus steppers. As scores are entered, the app automatically classifies each result (hole-in-one, eagle, birdie, par, bogey, double bogey, triple, and beyond), shows the running total relative to par, and updates a shared leaderboard.

## Features

- **Score entry tab** – Tap-friendly steppers for every hole, with par and yardage shown per hole and live "to par" totals for the front nine, back nine, and full round.
- **Leaderboard tab** – Ranks the groups by their total score so everyone can see who's leading at a glance.
- **Roster tab** – Lists all players organized into their groups.
- **Multiple tee options** – Switch between back, middle, and forward tees, each with its own yardages.
- **Celebration sounds** – Optional audio cues and voice clips play for notable results (birdie, eagle, hole-in-one, etc.), with a one-tap mute toggle. Audio files live in the `audio/` folder.
- **Saved progress** – Scores, the selected tee, and the sound preference are stored in the browser's `localStorage`, so a refresh or accidental close won't lose the round.
- **Installable feel** – Mobile web-app meta tags give it a full-screen, app-like experience when added to a phone's home screen.

## Running it

Because everything is contained in `index.html`, you can simply open that file in any modern browser, or host it on any static host. A live version is published via GitHub Pages.

## Tech

Plain HTML, CSS, and vanilla JavaScript — no frameworks or build step. The Web Audio API is used for tones, with pre-recorded voice clips layered on top for the fun reactions.
