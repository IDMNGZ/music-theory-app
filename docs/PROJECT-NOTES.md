# Music Theory Visualizer — Project Notes

**This is a living document.** Read it at the start of any new session working on this
app, and update it whenever a notable feature, convention, or decision changes.

Repo: `github.com/IDMNGZ/music-theory-app` · Live: `idmngz.github.io/music-theory-app/` ·
Local: `X:\APP_projects\music-theory-app`

For UI/UX design patterns and collaboration style, see the MTG Deck Builder handoff docs
at `X:\APP_projects\mtg-deckbuilder\docs\` — both `UI-DESIGN-AND-COLLABORATION-HANDOFF.md`
and `SYNC-ARCHITECTURE-HANDOFF.md` were written to travel to this project.

## Current shape of the app

Static single-file HTML/CSS/JS (`index.html`). No build step, no framework, no backend.
GitHub Pages deployment from `main` branch root.

**Current structure (pre-overhaul):**
- Splash screen: logo image, Enter + Venmo buttons, version footer
- Header: app title + subtitle, secondary-nav row (About/How To/Share/Sound/Resync),
  view-toggle row (Guitar/Keyboard/Circle), mode-tabs row (Scales/Chords/Progressions)
- Sticky controls bar: Root Note, Scale, Tuning dropdowns
- Main content: changes per mode/view combination

**Assets:**
- `index.html` — entire app (~2800+ lines)
- `IanD_BioPic.JPG` — bio photo used in About section
- `MV_Logo_1.png`, `MV_logo_2.png` — logo art (currently MV_logo_2 shown on splash)

## Modes and views

**Modes (primary content tabs):** Scales · Chords · Progressions
**Views (visualizer):** Guitar (fretboard SVG) · Keyboard (piano SVG) · Circle (Circle of Fifths SVG)
All 3 modes × 3 views work together.

## Audio engine

Web Audio API additive harmonic synthesis. Signal chain:
oscillators → harmonics → lowpass filter → [fuzz, guitar only] → bassBoost → noteGain
→ masterCompressor → dryGain / reverbNode → masterGain → destination

Guitar: fuzz (WaveShaperNode k=4), attack 0.01s
Keyboard: no fuzz, attack 0.045s
Both: vibrato LFO at 5Hz, depth ramps to 4 cents, bass boost lowshelf +7dB at 220Hz

Audio explicitly deferred for further tuning — user said "good enough for now."

## CSS design tokens

```
--bg:#0a0a0b  --surface:#111113  --surface2:#18181c  --surface3:#1f1f24
--border:#252529  --border2:#2e2e34
--text:#e4e2dd  --muted:#636268  --muted2:#4a494f  --muted-bright:#9c9aa4
--gold:#f0a500  --gold-dim:rgba(240,165,0,0.08)
```
Fonts: Space Grotesk (body), Space Mono (labels/mono)

## Version

`APP_VERSION` and `APP_VERSION_DATE` constants near bottom of `index.html` JS section.
Current: v2.4 (August 4, 2026). Bump with every push.

## Conventions

- **Commit messages explain *why*, not just *what***
- **Verify in browser before declaring done** — open `idmngz.github.io/MUSIC/` after push
- **Discuss design tradeoffs before building** — screenshots + annotation is the normal
  feedback format; address each annotated region separately
- **No sync/localStorage** — this app is purely stateless (sessionStorage only for
  splash visited flag)

## Known open items / deferred work

- **Audio tuning**: explicitly deferred. Will return in a future session.
- **Circle chord-card mini-previews**: when Circle view is active, chord-detail sub-panel
  falls back to keyboard-style mini preview. No user request to fix yet.
- **Major UI/UX overhaul in progress** (session started 2026-08-04): matching MTG Deck
  Builder visual patterns — landing page redesign, tab/nav restructure, rotating
  backgrounds, System tab, About page restructure.

## Feature ideas (discussed, not built)

| Idea | Notes |
|---|---|
| Rotating background images on splash | User will provide Midjourney art; structure = same as MTG app's landing-backgrounds.js pattern |
| Rotating backgrounds in app | All tab views get cycling background; user will provide art |
| Custom title font | User will provide font file |

## Open items from last session (pre-overhaul)

All previous content/functionality work complete and pushed as of v2.0.
Starting UI/UX overhaul session 2026-08-04.
