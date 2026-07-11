# app-assets — real SplitStream screenshots for the landing page

Curated captures from the live Android app (debug build, `com.splitstream.android`)
running on a Pixel emulator, season data 2026, next race Austrian GP / Red Bull Ring.
These fill the placeholder slots in `../SplitStream Landing.dc.html` (see handoff
`../README.md` §"Assets" and §5.5 Widget Catalog).

## Widget catalog slots (`#widgets` section)

Each widget was placed on a real home screen, captured, then cropped to its host
bounds with rounded corners and exported on a **transparent background** (RGBA PNG),
so it drops onto any section background (`#0E0E0E`, `#131313`, or a `#1A1919` catalog
card). All widgets are the **Dark** theme variant.

| Slot (`[ drop: … ]`) | File | Widget size | What it shows |
|---|---|---|---|
| Countdown | `widget-countdown.png` | 3x2 | Round + circuit + ticking `DD : HH:MM:SS` + next session row (Austrian GP) |
| Countdown Large | `widget-countdown-large.png` | 4x3 | Same, with the full weekend schedule (FP1-3, Q1-3, Race) |
| Standings | `widget-standings.png` | 3x2 | Driver table, team-color bars, points + gap-to-leader (ANT P1, 156) |
| Trivia | `widget-trivia.png` | 4x2 | Rotating F1 fact (1979 Villeneuve/Arnoux duel, Dijon) |
| Driver Stats | `widget-driver-stats.png` | 2x2 | Favourite driver season numbers (Antonelli, 156 pts, 5/6/4) |
| Lap Record | `widget-lap-record.png` | 4x2 | Circuit fastest lap (Red Bull Ring, 1:05.619, Sainz, McLaren) |

Notes for the catalog:
- Team-color theming is visible: teal Mercedes bars in Standings, orange McLaren accent
  in Lap Record, team dots in Driver Stats. Good support for the "Team-color theming" pill.
- The small moon glyph top-right of some cards is the in-widget Dark-theme indicator.

## Hero / phone-mockup slot

Full-screen app captures (1344x2992, status bar cleaned via SystemUI demo mode). Drop
into the in-phone screen slot (`[ drop: app home screen ]`).

| File | Screen |
|---|---|
| `phone-home.png` | Schedule home — Austrian GP hero + live countdown + session list (primary) |
| `phone-standings.png` | Championship standings screen (alternate / second-phone option) |

The hero's floating Standings chip and Countdown widget in the prototype can stay as the
illustrative overlays, or be swapped for `widget-standings.png` / `widget-countdown.png`.

## Regenerating / editing

Source raw screenshots and the crop script live in the session scratchpad (not committed).
Each widget card = crop of the launcher `AppWidgetHostView` bounds + a rounded-rect alpha
mask (radius ~70-80 px) on a transparent canvas. To recapture: place the widget on a home
screen over a dark area, screenshot with `adb exec-out screencap`, read the host bounds
from `uiautomator dump` (static widgets) or detect the `#1A1919` card by color (the
ticking Countdown widgets never reach UI-idle, so dump fails on them), then crop + mask.
