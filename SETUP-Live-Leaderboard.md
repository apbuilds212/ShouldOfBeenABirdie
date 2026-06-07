# Live Shared Leaderboard — Setup Guide

This turns "Should of Been a Birdie" into a **live, shared** scoreboard. Every guest opens one link and sees the leaderboard update in real time, while **one designated scorekeeper per group** enters the numbers.

**Two modes, zero risk:**
- **Local mode (default, right now):** scores live on each phone. Nothing to set up. The app works exactly as it does today.
- **Live mode:** paste a Firebase config (below) and the board syncs across all 24 phones.

You only need the two short setups below to switch on Live mode. Total time: ~12 minutes.

---

## Part A — Turn on the live board (Firebase) · ~10 min

Firebase's free **Spark plan** is more than enough for a one-day outing (1 GB stored, 10 GB downloads/month) and **requires no credit card**.

1. **Create a project.** Go to [console.firebase.google.com](https://console.firebase.google.com), sign in with any Google account, click **Add project**, name it (e.g. `tommy-50`), and finish. You can skip Google Analytics.

2. **Create the Realtime Database.** In the left menu open **Build → Realtime Database → Create Database**. Pick the location closest to you (United States is fine), and choose **Start in test mode** for now. Click Enable.
   - Copy the database URL it shows you — it looks like `https://tommy-50-default-rtdb.firebaseio.com`. You'll need it in step 4.

3. **Register a web app.** Click the gear icon → **Project settings**. Scroll to **Your apps** and click the **`</>`** (web) icon. Give it a nickname, click **Register app**. Firebase shows you a `firebaseConfig` block — leave this page open.

4. **Paste the config into the app.** Open `deploy/index.html` in any text editor and find the block near the top of the `<script>` that starts with `const FIREBASE_CONFIG`. Copy the matching values from Firebase. The one field that **must** be filled is `databaseURL`:

   ```js
   const FIREBASE_CONFIG = {
     apiKey:      "AIza...your value...",
     authDomain:  "tommy-50.firebaseapp.com",
     databaseURL: "https://tommy-50-default-rtdb.firebaseio.com",   // REQUIRED
     projectId:   "tommy-50",
     appId:       "1:1234...:web:abcd..."
   };
   ```

5. **Set the database rules.** Back in Realtime Database, open the **Rules** tab and paste this, then **Publish**. (Test mode auto-expires after 30 days; this keeps it open for the event.)

   ```json
   {
     "rules": {
       "events": {
         "$event": { ".read": true, ".write": true }
       }
     }
   }
   ```
   This is open read/write — perfectly fine for a private one-day outing. If you want to lock it down after the round, change both to `false` and re-publish.

6. **Set the scorekeeper code.** A few lines below the config in `index.html`:

   ```js
   const SCOREKEEPER_PIN = "5050";   // give this ONLY to your 6 scorekeepers
   ```
   Change it to whatever you like (or set it to `""` to skip the code entirely). Only people with this code can flip on Scorekeeper Mode and write to the board.

That's it — the app is now wired for live sync.

---

## Part B — Put it online so everyone can open it · ~2 min

The easiest path (no account needed):

1. Go to **[app.netlify.com/drop](https://app.netlify.com/drop)**.
2. Drag the entire **`deploy`** folder onto the drop zone.
3. Netlify gives you a public URL like `https://random-name-123.netlify.app`. That's your shareable link.
   - The folder is well under Netlify's limits (largest file ~0.5 MB), so it deploys instantly.
4. **Optional but recommended:** create a free Netlify account so the URL stays stable and you can rename it (e.g. `tommy-50-golf.netlify.app`) and re-drop updates later.

**Distribute it:** text the link to the group, or paste it into a free QR-code generator and print the QR for the first tee / clubhouse table so guests just scan and play.

> GitHub Pages works too if you prefer — but Netlify Drop is the fastest for a non-developer.

---

## Part C — On the day

- **Everyone** opens the link → Welcome note, Tee Times, live Leaderboard, and Sounds all work for all 24 guests, no setup on their end.
- Your **6 chosen scorekeepers** each do this once:
  1. Open the **Score** tab.
  2. Tap the **Scorekeeper Mode** switch → enter the code → type their name.
  3. Pick their **Group** and enter best-ball scores hole by hole.
- The header badge shows **● Live** when connected. Every score a scorekeeper enters appears on everyone's Leaderboard within a second, stamped **"kept by [name]"** for transparency.
- Everyone else's Score tab is **view-only** and shows their group's scores rolling in live.

---

## Quick test before game day

1. Open your Netlify URL on your phone **and** on a computer.
2. On one, turn on Scorekeeper Mode, pick Group 1, tap in a few scores.
3. Watch the Leaderboard update on the **other** device within a second. ✅

---

## Good to know

- **The code (PIN) is a soft gate**, meant to keep well-meaning guests from accidentally editing — not a security system. For a birthday outing that's exactly right.
- **Free tier is plenty:** 6 groups × 18 holes of tiny text updates won't come close to any limit.
- **No internet? No problem:** if a phone drops offline or Firebase isn't configured, the app automatically falls back to local mode and the badge reads "On this phone" or "Offline." Nothing breaks.
- **Updating the app later:** edit `deploy/index.html`, then drag the `deploy` folder onto Netlify again (or your account's Deploys page) to publish the new version.

---

*Sources: [Firebase pricing / Spark plan](https://firebase.google.com/pricing) · [Get started with Netlify Drop](https://docs.netlify.com/start/get-started-with-drop/)*
