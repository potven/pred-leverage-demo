# Pred → Boost leverage walkthrough (NBA 2027 Champion)

Client demo of Protofire's **Boost** leverage feature embedded in a pixel-perfect copy
of the Pred market page `pred.app/trade/nba-2027-champion`, featured outcome
**Oklahoma City Thunder LONG @ 25.5¢**. Wrapped in a two-chapter walkthrough
(*The feature* / *How it works (manual)*). Static site — no build step.

Kept fully separate from the seer and prophecy demos (own repo + own Vercel project).

## Files
- `index.html` — the walkthrough shell (loads `venue.html` in iframes via `?view=1|2|3`)
- `venue.html` — Pred snapshot + injected Boost feature (self-contained: `css/`, `fonts/`, `img/` all vendored)
- `css/ fonts/ img/` — vendored Pred + Google Fonts + RemixIcon assets (survive a Pred redeploy)

## Demo numbers (all derived from price 0.255 / base 400 / 1.4× / 50% LTV)
$400 base · 1.4× · **$560** exposure · **$160** borrowed · 1,569 → 2,196 Thunder shares ·
auto-protect below **15%** · health **1.75** · max boost 1.5×. Boost auto-unwinds ~1 week
before the 2027 Finals.

## Run locally
```
python3 -m http.server
# open http://127.0.0.1:8000/index.html   (http, not file://, so ?view params work)
```

## Deploy (fresh repo + fresh Vercel project — do NOT reuse seer/prophecy)
The local git repo already exists at `D:\git\pred-leverage-demo`.

```bat
:: 1) copy these built files into the repo working tree
robocopy "%USERPROFILE%\Claude\Projects\PredM Leverage capability\pred-leverage-demo" D:\git\pred-leverage-demo /E

:: 2) commit + push (create the empty GitHub repo potven/pred-leverage-demo first)
cd /d D:\git\pred-leverage-demo
git init
git add -A
git commit -m "Pred NBA 2027 Champion - Boost leverage demo"
git branch -M main
git remote add origin https://github.com/potven/pred-leverage-demo.git
git push -u origin main
```

Then in Vercel: **Add New -> Project -> import `potven/pred-leverage-demo`**,
framework preset **Other**, no build command, output = repo root,
project name **`pred-leverage`** -> deploys to `pred-leverage.vercel.app`.

After deploy, spot-check each chapter live and confirm the Boost block renders in the buy panel.
