# Task: Multiplication Tables SRS Web App

Build a single-page web app (pure HTML/CSS/JS, no build tools) for learning multiplication tables using a Spaced Repetition System (SRS).

## Core Requirements

### Learning Content
- Multiplication tables from 2×2 to 10×10 (all 81 combinations)

### UI Layout
- Large question display: "7 × 8 = ?" in big bold font, center of screen
- Numeric keypad on screen (0-9, backspace, enter/check) — tappable on mobile too
- Current answer displayed as typed (live feedback)
- Subtle progress indicator (e.g. "12/81 mastered")

### Interaction Flow
1. Question appears
2. User types digits via keypad or physical keyboard
3. After pressing Enter (or = button):
   - If correct: flash green, brief "✓" feedback, next question immediately
   - If wrong: flash red, show correct answer briefly, then next question
4. Speed should feel snappy — minimal delay between questions

### SRS / Timing Logic
Use a simple SM-2-inspired algorithm stored in localStorage:

**Answer quality based on timing + correctness:**
- Wrong answer → quality 0 (difficulty: "hard", interval resets to 1 day)
- Correct, > 3 seconds → quality 2 (difficulty: "insufficient", interval multiplies slowly)
- Correct, ≤ 3 seconds → quality 4 (difficulty: "acceptable")
- Correct, < 1.5 seconds → quality 5 (difficulty: "good/mastered")

**SRS fields per card:**
- `interval` (days, starts at 1)
- `easeFactor` (starts at 2.5)
- `dueDate` (timestamp)
- `lastQuality`

**Scheduling:**
- After each answer, update interval using SM-2 formula
- Next session: show cards due today first, then new cards
- When all today's cards are done, show a "Come back tomorrow!" screen with stats

### Visual Design
- Clean, minimal, modern
- Dark background (dark navy or charcoal)
- Large white/yellow question text (min 72px)
- Colored keypad buttons, rounded corners
- Green flash on correct, red flash on wrong
- Show timing feedback (e.g. "⚡ Fast!" / "✓ Good" / "🔄 Keep practicing")
- Mobile-friendly (works on phone screen)

### Data Persistence
- Store all card data in `localStorage` under key `mult-srs-data`
- Reset button (with confirmation) to start fresh

### GitHub Pages Deployment
- Everything must be in a single `index.html` file (inline CSS + JS)
- No external dependencies (no CDN, no npm, fully offline)
- The repo will be deployed as a GitHub Pages site from the `main` branch root

## File Structure
```
index.html   ← everything, single file
README.md    ← brief description + how to use
```

## After Building
1. `git add -A`
2. `git commit -m "Initial build: multiplication SRS web app"`
3. `git push origin main`

Then run: `openclaw system event --text "Done: mult-srs web app built and pushed to GitHub" --mode now`
