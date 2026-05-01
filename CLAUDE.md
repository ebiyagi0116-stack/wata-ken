# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Single-file static HTML/CSS flyer generator for **こどもパントリー新聞** (Children's Pantry Newspaper), a Japanese charity event run by "このまちくらす" in Toyohashi. Each issue is a standalone `index.html` that renders a newspaper-style Instagram post.

There is no build step, no package manager, and no JavaScript. Open `index.html` directly in a browser to preview.

## Instagram export workflow

The page renders a single `.newspaper` div at **1080×1080 px** (exact Instagram square format), scaled down to 50% for comfortable screen preview via `transform: scale(0.5); transform-origin: top left`. To export, use a browser screenshot tool or DevTools device emulation at 1080×1080 with no scaling — remove the `transform: scale(0.5)` rule temporarily if needed.

## Layout architecture

The `.newspaper` div uses a three-section vertical stack:

```
.masthead        ← newspaper nameplate + date/tagline
.kicker-bar      ← green accent banner
.body            ← CSS Grid: col-left | col-divider (1px) | col-right
.footer          ← contact info row
```

The `.body` grid is `grid-template-columns: 2fr 1px 1.4fr`. The 1px `.col-divider` div acts as a visual rule — it is a real DOM element, not a border.

## Design conventions

| Token | Value | Usage |
|---|---|---|
| Background parchment | `#f5f0e0` | Page, masthead, footer bg |
| Outer bg | `#d4c89a` | `body` background |
| Dark ink | `#1a1a1a` | Borders, headlines |
| Red accent | `#c0392b` | Key dates, item names, labels |
| Green accent | `#2e6b2e` | Kicker bar, section titles, event box |
| Orange badge | `#e67e22` | "無料配布" (free) circular badges |

Fonts loaded from Google Fonts:
- `'Noto Serif JP'` — body serif (headings, large display text)
- `'Noto Sans JP'` — sans-serif (labels, metadata, supporting copy)

Font weights in use: 400, 700, 900.

## Updating event content

All event-specific content (date, items, venue, times) is hardcoded inline in the HTML. There are no templates or data files. To create a new issue, duplicate `index.html` and edit the text nodes and inline styles directly.

The `.free-badge` circle (無料配布 / free badge) is `position: absolute; top: -10px; right: -10px` relative to its `.item-box` parent — the parent needs `position: relative` to anchor it correctly.
