
# Tachyon House Points Calculator

A lightweight, responsive web app for tracking points across Tachyon's four houses: **ALPHA, INFER, MATRIX, and LAYER**. It records point awards, totals each house's score, ranks the houses, and highlights the current leader.

## Features

- Award points to a selected house.
- Add new points to the existing total (scores are not overwritten).
- View current totals for all four houses.
- Automatically rank houses from highest to lowest score.
- Detect and display ties for the lead.
- View a timestamped history of point awards and the total after each award.
- Save scores in browser `localStorage`, so they remain after refresh in the same browser on the same device.
- Clear only the history, or reset all scores and history after a confirmation prompt.
- Responsive layout for desktop, tablet, and mobile screens.
- Validate entries: points must be a positive whole number.

## Technology stack

- **HTML5** — page structure and form controls.
- **CSS3** — layout, responsive styles, and house-specific visual design.
- **Vanilla JavaScript** — input validation, scoring, sorting, tie detection, rendering, history, and persistence.
- **Browser localStorage** — local persistence without a database or server.

No package installation, build step, API key, or backend is required.

## How to run

### Option 1: Open directly

1. Download or clone this repository.
2. Open `index.html` in a modern browser such as Chrome, Edge, or Firefox.
3. Select a house, enter a positive whole number, and click **Award points**.

### Option 2: Run a local web server (recommended)

If Python is installed, open a terminal in the project directory and run:

```bash
python -m http.server 8000
```

Then open <http://localhost:8000> in your browser.

## How it works

1. The application starts with a score of `0` for each house unless saved scores exist in this browser.
2. When a user submits a valid entry, the program adds the entered value to that house's current score.
3. It appends a history record containing the house, points awarded, timestamp, and updated total.
4. The summary cards, house scoreboard, leaderboard, and history are re-rendered immediately.
5. The updated scores and history are saved to `localStorage`.

## How ranking is calculated

The app sorts the four house names by their scores in **descending order**. In JavaScript, the core comparison is:

```javascript
Object.keys(HOUSES).sort((a, b) => state.scores[b] - state.scores[a] || a.localeCompare(b));
```

- `state.scores[b] - state.scores[a]` puts the house with the larger score first.
- If two houses have the same score, `a.localeCompare(b)` orders them alphabetically for a stable display.
- A separate check finds all houses whose score equals the maximum score. If multiple houses share a non-zero maximum, the summary reports a tie and each leading house is marked **Tied for first**.
- If all scores are zero, no winning house is announced yet.

The alphabetic tie-break only determines display order; tied houses still share the lead.

### Sample calculation

Suppose the recorded awards produce these totals:

| House | Total points | Displayed position |
|---|---:|---:|
| MATRIX | 80 | First |
| INFER | 65 | Second |
| ALPHA | 50 | Third |
| LAYER | 30 | Fourth |

**Winner: MATRIX with 80 points.** See [`sample-output.md`](sample-output.md) and the screenshots in [`screenshots/`](screenshots/).

## Sample output / screenshots

Desktop sample: [`screenshots/leaderboard-sample.png`](screenshots/leaderboard-sample.png)

Mobile sample: [`screenshots/mobile-sample.png`](screenshots/mobile-sample.png)

The screenshots show example data to demonstrate the expected leaderboard. The project starts with a clean scoreboard for a new browser profile.

## Reset and data notes

- **Clear history** removes the transaction list but keeps all house totals.
- **Reset all** removes every house's score and the full history after confirmation.
- Data is stored only in the current browser's local storage. It is not synchronized with another computer or shared between organizers. Clearing browser site data can remove saved scores.

## Manual test checklist

- [ ] Award points to each of the four houses and check that its total updates.
- [ ] Award points to the same house twice and confirm the values add together.
- [ ] Confirm leaderboard order changes when a lower-scoring house overtakes another.
- [ ] Give two houses the same highest score and confirm both show as tied for first.
- [ ] Try an empty, zero, negative, decimal, or non-numeric input; invalid awards should not be recorded.
- [ ] Refresh the page and confirm scores/history remain in the same browser.
- [ ] Clear history and confirm scores stay unchanged.
- [ ] Reset all and confirm all totals return to zero.

## Suggested GitHub submission steps

1. Create a new **public** GitHub repository named `tachyon-house-points-calculator` (unless your instructor specifies another visibility setting).
2. Upload `index.html`, `README.md`, `sample-output.md`, `.gitignore`, and the `screenshots/` folder. Or use Git commands:

   ```bash
   git init
   git add .
   git commit -m "Build Tachyon house points calculator"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/tachyon-house-points-calculator.git
   git push -u origin main
   ```

   Replace `YOUR-USERNAME` with your GitHub username. Create the empty repository on GitHub first; do not add a second README there if you already have this one locally.

3. To publish a live website with GitHub Pages, open the repository's **Settings → Pages**, choose **Deploy from a branch**, select `main` and `/ (root)`, then save. After GitHub finishes deployment, the Pages URL will appear in that section.
4. Submit the repository URL and, if requested, the deployed GitHub Pages URL.

## Project structure

```text
tachyon-house-points-calculator/
├── index.html
├── README.md
├── sample-output.md
├── .gitignore
└── screenshots/
    ├── leaderboard-sample.png
    └── mobile-sample.png
```
