# SleeperStack — Portfolio Exposure Tracker

A single-page tool that scans all your active 2026 Sleeper leagues and shows which players you have the most shares of, complete with KeepTradeCut values, ownership percentages, and waiver wire suggestions.

No backend, no login, no install — just upload two files to GitHub and share the link.

---

## Features

### Portfolio Exposure
- 🔍 Enter any Sleeper username to scan all your 2026 NFL leagues at once
- 📊 Players ranked from highest to lowest share count
- 📈 Ownership percentage shown next to each player's share count (e.g. `7 (31.8%)`) — calculated against the number of leagues currently in view
- 👆 Click any player card to expand and see the exact leagues you own them in
- 🔗 Click any league name to jump directly to that league on Sleeper.com
- 🖼️ Auto-loads player headshots from the Sleeper CDN

### League Type Filtering
- ✅ Filter your results by league type using checkmark toggles:
  - **Dynasty Lineup**
  - **Dynasty Bestball**
  - **Redraft Lineup**
  - **Redraft Bestball**
- League types are auto-detected from your league settings (taxi slots, best ball flag, etc.)
- All stats and percentages update live as you toggle filters

### Stats Dashboard
- **Leagues Scanned** — total number of leagues found on your account
- **Leagues in View** — number of leagues visible under your current filters
- **Unique Players** — how many distinct players appear across your filtered leagues

### KeepTradeCut Integration
- 💰 KTC values displayed on every player card, color-coded by tier:
  - 🟢 **Elite** — 7,000+
  - 🔵 **High** — 4,000–6,999
  - 🟡 **Mid** — 2,000–3,999
  - 🔴 **Low** — under 2,000
  - ⬜ **N/A** — player not found in KTC data
- Sort your entire list by **KTC Value** instead of share count using the sort toggle
- KTC data is loaded from a `ktc_values.csv` file you keep updated in your repo

### Waiver Wire Suggestions
- 🔄 For any player with a KTC value under 2,000 (or no KTC value at all), the tool automatically scans the waiver wire in each of your **dynasty leagues** and suggests the best available replacement
- Suggestions show the player's position, name, and KTC value badge
- "Best Available on Waivers" appears inline below the league name when you expand a player card
- Only QB, RB, WR, and TE are considered for suggestions — kickers, defense, and IDP positions are excluded
- Waiver results are cached per league during the scan so the same league is never fetched twice
- Works by fetching all rostered players in the league and subtracting from the full player database, ensuring accurate results including pre-draft rookies

---

## Files Required

| File | Purpose |
|------|---------|
| `index.html` | The entire app — all HTML, CSS, and JavaScript in one file |
| `ktc_values.csv` | KeepTradeCut player values, must be in the same folder as `index.html` |

The CSV must have exactly two columns with this header:
```
Player_Sleeper,KTC_Value
Josh Allen,9993
Bijan Robinson,9982
...
```

---

## How to Host on GitHub Pages

### Step 1: Create a GitHub account
If you don't have one: https://github.com/signup

### Step 2: Create a new repository
1. Go to https://github.com/new
2. Name it something like `sleeper-portfolio`
3. Set it to **Public**
4. Click **Create repository**

### Step 3: Upload both files
1. On your new repo page, click **uploading an existing file**
2. Drag and drop both `index.html` and `ktc_values.csv` into the upload area
3. Scroll down and click **Commit changes**

### Step 4: Enable GitHub Pages
1. Go to your repo → **Settings** → **Pages** (left sidebar)
2. Under **Source**, select **Deploy from a branch**
3. Choose branch: `main`, folder: `/ (root)`
4. Click **Save**

### Step 5: Share!
After ~60 seconds your tool will be live at:
```
https://YOUR-GITHUB-USERNAME.github.io/sleeper-portfolio/
```

Anyone can use it by entering their own Sleeper username — no account required.

---

## Keeping KTC Values Updated

When you pull fresh KTC data from your automated script, just upload the new `ktc_values.csv` to your GitHub repo to replace the old one. The app will use the updated values on the next scan automatically.

To update a file in GitHub:
1. Go to your repo and click on `ktc_values.csv`
2. Click the pencil icon (Edit) or drag a new file over it
3. Commit the change — GitHub Pages updates within seconds

---

## How It Works

1. Looks up your Sleeper user ID via the public API
2. Fetches all your NFL leagues for the 2026 season
3. Downloads the full Sleeper player database (~5MB, cached for the session)
4. Scans each league roster to find your team
5. Counts how many leagues each player appears on and builds the ranked list
6. Loads `ktc_values.csv` and matches player names to KTC values
7. For dynasty leagues containing low-value or unranked players, fetches all rosters to determine true free agents, then finds the highest-KTC available QB/RB/WR/TE on the wire

---

## Notes

- The Sleeper player database takes a few seconds to load on first scan — subsequent scans in the same session are faster
- Name matching between Sleeper and KTC handles common edge cases: Jr./Sr./II/III suffixes, apostrophes, hyphens, and minor formatting differences
- Works for any public Sleeper username — useful for comparing exposure with friends
- League links open directly on Sleeper.com

---

## Tech Stack

Pure HTML + CSS + Vanilla JavaScript. No build step, no npm, no dependencies.
Uses the [Sleeper public API](https://docs.sleeper.com/).
