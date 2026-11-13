# web-playground

Self-contained browser demos. Each is one `index.html` with no build step, no CDN, no
images and no audio files — open it in a browser and it runs.

| Demo | Path | Size | Written by |
|---|---|---|---|
| Tetris / 俄罗斯方块 | [`tetris/index.html`](tetris/index.html) | 44,388 B | OpenAI Codex (`gpt-6.1-sol`) |
| Pelican on a bike | [`pelican-bike/index.html`](pelican-bike/index.html) | 63,846 B | Google Antigravity |

## How they were made, and how they were checked

Both were written by autonomous coding agents. Neither agent could open a browser in its
own sandbox, so the interactive check was done from the outside, in a real Chromium
window with real keyboard and mouse input over a local `python3 -m http.server`:

- **Tetris** — the agent ran 22 Node self-tests (7-bag randomizer, 168 wall-kick
  rotations, scoring tables, a 6000-frame / 120-second simulated game) and honestly
  marked browser validation as *not run*, because its sandbox refused to start Chromium.
  Verified in the browser: rendering, `←` `→` move, `↑`/`X` rotate, `↓` soft drop,
  `Space` hard drop, `C` hold, `P` pause overlay, `R` restart, touch buttons, line-clear
  scoring (rows 0→1, score 0→100, high score kept), ghost landing preview, and
  game-over-then-any-key restart. Passed.
- **Pelican on a bike** — the agent's own self-tests were *zero* (Antigravity can write
  files but cannot execute commands), so everything below is from the browser check:
  coastal scene and HUD (speed / cadence / gradient) render; sprint button ramps
  28 → 39 → 46 km/h with smooth acceleration and cadence 39 → 54 RPM; uphill +5° cuts
  46 → 36 km/h and tilts the frame; `U` switches to downhill −5°; `1` drops to the slow
  gear and speed settles toward the slider value; `Space` pauses. Passed.

## Try one

```
git clone https://github.com/bjxudjdbxkdj/web-playground.git
cd web-playground
python3 -m http.server 8000
# open http://localhost:8000/tetris/  or  http://localhost:8000/pelican-bike/
```

Or download a single file and double-click it:

- https://raw.githubusercontent.com/bjxudjdbxkdj/web-playground/main/tetris/index.html
- https://raw.githubusercontent.com/bjxudjdbxkdj/web-playground/main/pelican-bike/index.html
