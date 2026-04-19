# ♟ Chess Puzzles Trainer

An interactive chess tactics trainer built with real puzzles from the [Lichess open puzzle database](https://database.lichess.org/#puzzles). No backend required — fully self-contained static HTML.

## Features

- **15 real Lichess puzzles** — 5 Easy (800–1000 ★), 5 Medium (1500–1800 ★), 5 Hard (2200+ ★)
- **Renew button** — shuffles a fresh set of 5 from an embedded pool of 30 per difficulty tier, no page reload needed
- **Interactive board** — click to select pieces, legal-move hints, opponent auto-responds
- **Two-stage hint** — first click shows which piece to move; second click plays the answer automatically
- **Board feedback** — green flash on correct moves, red flash on wrong, border stays green when solved
- **Light / Dark theme** — toggle between classic wooden board (light) and teal night mode (dark); puzzle preview cards update instantly
- **Puzzle navigation** — dot indicators show progress and solved state per difficulty tab

## Tech Stack

| Layer | Tool |
|---|---|
| Chess logic | [chess.js 0.10.3](https://github.com/jhlywa/chess.js) via CDN |
| Rendering | Vanilla JS + HTML5 Canvas (320×320 px per preview) |
| Fonts | [Cinzel](https://fonts.google.com/specimen/Cinzel) + [EB Garamond](https://fonts.google.com/specimen/EB+Garamond) via Google Fonts |
| Hosting | [Vercel](https://vercel.com) (static) |

## Project Structure

```
chess-puzzles/
├── index.html      # Entire app — self-contained single file
├── vercel.json     # Vercel deployment config
├── .gitignore
└── README.md
```

## Deploy to Vercel

### Option A — Vercel + GitHub (recommended)

1. Fork or push this repo to GitHub
2. Go to [vercel.com/new](https://vercel.com/new) → Import Git Repository
3. Select this repo — Vercel auto-detects it as a static site
4. Click **Deploy** — no build settings needed

### Option B — Vercel CLI

```bash
npm i -g vercel
vercel
```

### Option C — One-click

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/YOUR_USERNAME/chess-puzzles)

> Replace `YOUR_USERNAME` with your GitHub handle after pushing.

## Regenerating Puzzles

The puzzles are embedded at build time from the Lichess CSV. To regenerate with fresh random puzzles:

```bash
# Download the latest Lichess puzzle database
curl -O https://database.lichess.org/lichess_db_puzzle.csv.zst
zstd -d lichess_db_puzzle.csv.zst

# Generate a new index.html with fresh puzzles
python3 generate_chess.py lichess_db_puzzle.csv index.html
```

The script `generate_chess.py` (not included in this repo) samples 30 puzzles per difficulty tier and embeds them into the HTML. The in-browser Renew button then reshuffles those 30 into fresh sets of 5 without any server round-trip.

## License

Puzzle data © [Lichess.org](https://lichess.org) — released under [CC0](https://creativecommons.org/publicdomain/zero/1.0/).  
Code: MIT License.
