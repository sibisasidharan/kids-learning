# kids-learning

A small shelf of browser-based learning games, hosted on GitHub Pages. The root `index.html` is the landing page kids arrive at; each game lives in its own folder below it.

## Games

| Game | Path | What it practises |
| --- | --- | --- |
| [Times Table Time Trial](multiplication/) | `/multiplication/` | Multiplication tables 1–12, against the clock |

## Running it locally

No build step and no dependencies — open `index.html` in a browser and it works.

To exercise the links exactly as GitHub Pages serves them, run a static server from the repo root:

```bash
python3 -m http.server 8000
```

Then visit <http://localhost:8000>.

## Adding a game

Create a folder, put a self-contained `index.html` in it, and add a card to the shelf in the root `index.html`. See `CLAUDE.md` for the conventions that keep the games consistent — in particular the ASCII-only rule and the theming tokens.
