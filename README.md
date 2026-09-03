# Times Table Time Trial

A single-file multiplication practice game for kids. Open `index.html` in any browser — no build step, no server, no dependencies.

## What it does

- **Pick the tables** for a session — tap any of 1–12, or use a preset (Starter 2/5/10, Building up 3/4/6, Tricky ones 6–9, Big ones 11/12, Everything).
- **Pick the length** — 10, 20, 30 or 50 questions — and whether facts go up to ×10 or ×12.
- **Instant feedback** after each answer: correct answers flash green with a bit of praise and move on quickly; wrong ones flash red, show the correct fact, and hold for a moment so it registers.
- **A session timer** runs the whole set, with progress pips showing right/wrong at a glance.
- **Best times are remembered** per combination of tables + question count + range. Beating one shows the exact seconds saved, plus confetti.
- **Records need a perfect run.** Guessing fast doesn't set a record — this keeps accuracy and speed pulling in the same direction.
- **Drill the tricky ones** — after a session with mistakes, one button rebuilds a set from just the facts that were missed.

## Input

Works with the on-screen keypad (tap/click) or a physical keyboard: digits to type, `Backspace` to delete, `Enter` to check.

## Notes

- Best times are stored in `localStorage`. If storage is unavailable (some sandboxed embeds), it falls back to in-memory records that last for the browser session.
- Sound is a short synthesised tone via the Web Audio API, toggleable on the setup screen.
- Light and dark themes both supported; follows the system setting.
