<img width="1091" height="821" alt="Looks" src="https://github.com/user-attachments/assets/7ce28a01-854e-4e83-971e-e3cfb429a496" />
[README.md](https://github.com/user-attachments/files/34942125/README.md)
# Fortnite Pirate Token Cope
# Pirate Token Drop Simulator

A dark-mode, gold-and-pirate themed web app that simulates the odds of pulling a **Pirate Token** with a base drop rate of **1 in 137,500**. Pick a lucky number, choose a luck multiplier, and roll until the number comes up.

Everything lives in a single `index.html` file: no build step, no dependencies, no network requests.

<!-- Add a screenshot: ![Screenshot](screenshot.png) -->

## Features

- **Luck multipliers:** 1x (1 in 137,500), 1.5x (1 in 91,667), 2x (1 in 68,750). The valid number range updates with the odds.
- **Target selection:** type your own lucky number or press **Randomize target**.
- **Single roll:** one attempt, shows the rolled number.
- **Auto-roll until hit:** runs in batches with `requestAnimationFrame` so the browser never freezes. Includes a **Stop** button and a speed slider (1 to 100,000 rolls per frame).
- **Reset:** clears all stats.
- **Live stats:** total attempts, elapsed time, cumulative probability `1 - (1 - p)^n`, and luck status ("Under odds" or "Dry streak").
- **Recent rolls log** and a celebratory banner with confetti when the token drops.
- Respects `prefers-reduced-motion`.

## Run it

**Locally:** download `index.html` and double-click it. It opens in your default browser.

**With GitHub Pages:**
1. Push this repo to GitHub.
2. Go to **Settings > Pages**.
3. Under **Build and deployment**, set the source to **Deploy from a branch**, choose `main` and `/ (root)`, then save.
4. Your site will be live at `https://<your-username>.github.io/<repo-name>/`.

## How it works

- **Randomness:** each roll uses `crypto.getRandomValues` with rejection sampling, so every number in range is equally likely (no modulo bias). Rolls are independent: nothing nudges a result toward or away from your target.
- **Probability:** the displayed chance of having hit by now is `1 - (1 - p)^n`, where `p = 1 / range` and `n` is your attempt count.
- **Luck status:** "Under odds" until you pass the expected number of rolls (the range size), then "Dry streak" with the multiple of expected rolls.

## Customize

The odds are defined near the top of the script in `index.html`:

```js
var BASE = 137500;
var RANGES = {"1":137500,"1.5":91667,"2":68750};
```

Edit `RANGES` to change the odds or add more luck modes (and add a matching button in the `#luckSeg` group).

## Limitations

- The 1 in 137,500 rate and the luck multipliers are inputs, not verified game data. The 1.5x figure is 137,500 / 1.5, rounded.
- Real games may use pity timers or hidden mechanics that this simulator does not model.
- In fast auto-roll the log shows a sample of rolls; the attempt counter and hit check still count every roll.

## License

MIT. Use it however you like.
