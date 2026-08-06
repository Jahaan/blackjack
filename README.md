# Blackjack Odds Desk

A self-contained blackjack expected-value dashboard (single static `index.html`, no build step).

**Rules modeled:** 6 decks · dealer hits soft 17 · late surrender · double after split · blackjack pays 3:2.

## What's here
- `index.html` — the entire app (HTML + CSS + JS inline). A recursive solver computes win/push/lose
  and EV for stand/hit/double/split/surrender, an EV heatmap for every starting hand vs. dealer up card,
  and a Hi-Lo true-count adjustment.
- `vercel.json` — static hosting config (clean URLs, no-cache revalidate).

## Deploy on Vercel (Git auto-deploy)
1. Push this repo to GitHub (see below).
2. In the Vercel dashboard: **Add New → Project → Import** this repo.
3. Framework preset: **Other**. Root directory: `./`. No build command, no output dir — it's static.
4. **Deploy.** Every future `git push` to the default branch redeploys automatically.

## Push to GitHub
```bash
gh repo create blackjack-odds --public --source=. --push   # with the GitHub CLI
# — or, manually —
git remote add origin git@github.com:<you>/blackjack-odds.git
git push -u origin main
```

## Local preview
```bash
python3 -m http.server 4599
# open http://localhost:4599
```
