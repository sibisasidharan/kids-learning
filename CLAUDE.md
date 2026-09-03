# kids-learning

Browser-based learning games for a child, hosted on GitHub Pages.

## Layout

```
index.html              landing page - the shelf of games, served at /
multiplication/         Times Table Time Trial
```

GitHub Pages serves the root `index.html` first, so it must stay the landing page. Each game gets its own folder with a self-contained `index.html`, reached at `/<folder>/` — link to the folder with a trailing slash, not to `index.html`, so the URL stays clean.

Adding a game means creating the folder and adding one `<a class="game">` card to the shelf in the root `index.html`. The landing page shares the game's palette and typefaces deliberately; keep new cards on the same tokens so the site reads as one thing.

## Architecture

Each game is **one self-contained HTML file** — markup, CSS and JS inline, no build step, no package manager, no dependencies, no server. Open the file directly in a browser and it works.

Keep it that way. It means the games run from a USB stick, an email attachment, or GitHub Pages with equal ease, and there is nothing to maintain between the idea and the child playing it. Reach for a bundler or a framework only if a game genuinely cannot be built without one — and say why first.

The one permitted external request is Google Fonts. Everything else must be inline.

## Files must be pure ASCII

Non-ASCII characters in these files have already caused one visible bug: without a charset declaration a browser decodes UTF-8 as Latin-1, and `×` renders as `Ã—` in the middle of every question.

Write `&times;` `&middot;` `&ndash;` `&mdash;` in markup, and the equivalent `\u00d7` `\u00b7` `\u2013` `\u2014` escapes in JavaScript strings.

Check before committing:

```bash
grep -rn '[^\x00-\x7F]' --include='*.html' .
```

No output means clean. `<meta charset="utf-8">` is present too, but it is a backstop, not the fix.

## Theming

Colours are CSS custom properties defined in three places, and all three must stay in sync:

1. bare `:root` — the complete light palette
2. `@media (prefers-color-scheme: dark) { :root:not([data-theme="light"]) }` — dark via OS setting
3. `:root[data-theme="dark"]` — dark via an explicit stamp

Never give a colour its only definition inside a media query or a `[data-theme]` block; a page rendered in the un-stamped default state will pick up one theme's text on the other theme's background. When text sits on an accent-coloured surface, use `var(--on-accent)` rather than hardcoding `#fff` — that token is what keeps button labels legible in both themes.

## Persistence

Best times go through a `store` wrapper that try/catches `localStorage` and falls back to an in-memory object. Sandboxed embeds (anything served from a `data:` URL) throw on storage access, and an unguarded call breaks the whole game. Any new persisted state must go through the same wrapper.

## Writing for the player

The audience is a child, and the parent configuring the session. Praise is short and varied ("Nailed it!", "Bang on!"). A wrong answer shows the correct fact and holds on screen longer than a correct one, so the right answer is what gets read.

Game rules should not reward the wrong behaviour. In the multiplication game, records only count on a perfect run — otherwise the fastest strategy is to mash wrong answers, and the timer would teach the opposite of the point. Apply the same test to any new scoring.

## Verifying a change

There are no tests. Serve the repo (`python3 -m http.server 8000`) rather than opening files directly, so relative links behave as they do on Pages, then actually play the game. Check both themes, a narrow viewport, keyboard input as well as taps, and every end-of-session branch (new record, first record, perfect but slower, imperfect run) — those branches are easy to break and only visible at the end of a full run.

## Git

Default branch is `master`; work has been landing on topic branches like `multiplication-game`. Don't commit or push unless asked.
