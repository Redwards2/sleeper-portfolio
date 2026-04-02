# sleeper-portfolio
# SleeperStack — Portfolio Exposure Tracker

A single-page tool that scans all your active 2026 Sleeper leagues and shows which players you have the most shares of, filterable by league type.

## Features

- 🔍 Enter any Sleeper username to scan their roster exposure
- 📊 See every player you own ranked by share count
- ✅ Filter by league type: Dynasty Lineup, Dynasty Bestball, Redraft Lineup, Redraft Bestball
- 👆 Click any player to expand and see exactly which leagues you own them in
- 🔗 Click a league name to jump directly to that league on Sleeper
- 🖼️ Auto-loads player headshots from Sleeper CDN
- 🌐 No backend, no login required — runs entirely in the browser using Sleeper's free public API

---

## How to Host on GitHub Pages (share with friends in ~5 minutes)

### Step 1: Create a GitHub account
If you don't have one: https://github.com/signup

### Step 2: Create a new repository
1. Go to https://github.com/new
2. Name it something like `sleeper-portfolio`
3. Set it to **Public**
4. Click **Create repository**

### Step 3: Upload the file
1. On your new repo page, click **uploading an existing file**
2. Drag and drop `index.html` into the upload area
3. Scroll down and click **Commit changes**

### Step 4: Enable GitHub Pages
1. Go to your repo → **Settings** → **Pages** (left sidebar)
2. Under **Source**, select **Deploy from a branch**
3. Choose branch: `main`, folder: `/ (root)`
4. Click **Save**

### Step 5: Share!
After ~60 seconds, your tool will be live at:
```
https://YOUR-GITHUB-USERNAME.github.io/sleeper-portfolio/
```

Share that URL with your friends — anyone can use it by entering their own Sleeper username.

---

## How It Works

1. Looks up your Sleeper user ID via the public API
2. Fetches all your NFL leagues for the 2026 season
3. Downloads the full Sleeper player database (cached in memory for the session)
4. Scans each league for the roster belonging to your user ID
5. Counts how many leagues each player appears on and sorts highest to lowest
6. League type (Dynasty vs Redraft, Lineup vs Bestball) is auto-detected from league settings

## Notes

- The Sleeper player database is ~5MB and takes a few seconds to load on first scan
- Subsequent scans in the same browser session are faster (player DB stays loaded)
- Works for any public Sleeper username — great for comparing exposure with your league mates
- League links open directly on Sleeper.com

---

## Tech Stack

Pure HTML + CSS + Vanilla JavaScript. No build step, no npm, no dependencies.
Uses the [Sleeper public API](https://docs.sleeper.com/).
