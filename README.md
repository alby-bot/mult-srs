# Multiplication Tables SRS (2x2 to 10x10)

Single-page web app for practicing all 81 multiplication facts using a simple SM-2-inspired spaced repetition system.

## Features
- Covers `2×2` through `10×10` (81 cards)
- Large central prompt with live typed answer
- On-screen numeric keypad + physical keyboard support
- Speed-aware feedback (`⚡ Fast!`, `✓ Good`, `🔄 Keep practicing`)
- SRS card scheduling saved in `localStorage` key `mult-srs-data`
- Progress indicator and reset button
- "Come back tomorrow!" completion screen when no cards remain for today

## Usage
1. Open `index.html` in a browser.
2. Answer each prompt using keypad or keyboard digits.
3. Press `Enter` (or `=` button) to submit.
4. Correct/incorrect feedback is shown, and the next card appears immediately.

## Deployment
This project is fully self-contained in:
- `index.html` (HTML + CSS + JS)
- `README.md`

It is ready for GitHub Pages deployment from the root of the `main` branch.
