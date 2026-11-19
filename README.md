# Blackjack Odds Desk

A self-contained blackjack expected-value dashboard (single static `index.html`, no build step).

**Rules modeled:** 6 decks · dealer hits soft 17 · late surrender · double after split · blackjack pays 3:2.

## What's here
- `index.html` — the entire app (HTML + CSS + JS inline). A recursive solver computes win/push/lose
  and EV for stand/hit/double/split/surrender, an EV heatmap for every starting hand vs. dealer up card,
  and a Hi-Lo true-count adjustment.
- `trainer.html` — **Count Trainer.** An auto-dealt shoe game for practicing Hi-Lo counting:
  - Deals like a real table (2–8 decks, cut card, optional bot players who play basic strategy) and waits for your
    decisions, made with real table signals on the felt (mouse or touch):
    | Decision | Motion |
    |---|---|
    | Hit | Tap the felt |
    | Stand | Wave back and forth (fires as soon as you reverse) |
    | Double | Drag a chip from your stack onto your bet |
    | Split | Draw a V |
    | Surrender | Draw one straight line behind your chips |
    | Insurance / decline | Drag a chip onto the insurance line / wave it off |
    | Next hand | Tap the felt |

    Keyboard shortcuts (`H S D P R`, `I`/`N`, `Space`) also work, and on-screen buttons can be re-enabled in settings.
  - Before each hand you place a bet (tap your chip stack / the bet circle, quick chips, or keys 1–9) and it's graded
    against a Hi-Lo ramp: bet (true count − 1) units, min 1, capped at your spread (1–4, 1–8 or 1–12).
  - Bets within 1 unit of the ramp count as correct (within 2 once the ramp is 4+ units, i.e. TC +5 and up), and bet sizing is tracked in its own accuracy bar (not the mistake log).
  - Before every reshuffle you're asked for your final running count for the shoe, even with regular quizzes off.
  - A Start screen appears before the first hand and again whenever the shoe is reshuffled.
  - Grades every decision against basic strategy for these rules, with an option to grade Illustrious 18 / Fab 4 index plays.
  - Quizzes you on the running count every few hands (switchable to true count or both in settings; estimate decks left from the discard tray for true count).
  - A **Net units** line chart plots your running total after every hand (hover for any hand's value).
  - Tracks accuracy by hand type, recent mistakes, repeat leaks and a quiz log (saved in your browser's localStorage).
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
