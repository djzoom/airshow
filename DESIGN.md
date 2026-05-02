---
name: Air Show Planner
inspired_by: Claude (Anthropic)
last_updated: 2026-05-02
---

# DESIGN.md — 飞行表演规划系统

A DESIGN.md spec for AI coding agents (Claude Code, Cursor, Kiro etc) to
keep the UI of this project visually consistent. Drop it in the project
root; agents read it before generating any new component.

Format follows the conventions catalogued at https://getdesign.md and
https://github.com/VoltAgent/awesome-design-md.

---

## 1 · Visual Theme & Atmosphere

Editorial-tech, warm and quiet. The 3D viewport carries the spectacle;
chrome stays out of the way like a printed program. Inspired by
claude.ai: paper-grade neutrals, a single terracotta accent, generous
whitespace, no neon. No glass, no gradients in chrome, no glow except
on smoke trails.

Mood words: **calm, precise, warm, editorial, instrument-grade**.

---

## 2 · Color Palette & Roles

| Token | Hex | Use |
|---|---|---|
| `--bg`        | `#F7F5F2` | App background, planner, cards |
| `--bg-elev`   | `#FFFFFF` | Raised surfaces (drawer, dropdown) |
| `--bg-mute`   | `#EFEAE3` | Subtle row background, hover |
| `--ink`       | `#1A1C1E` | Primary text, headlines |
| `--ink-mute`  | `#6C7278` | Secondary text, labels |
| `--ink-faint` | `#A6ABB2` | Tertiary text, hint, separators |
| `--rule`      | `#E6E1D8` | 1px borders, dividers |
| `--accent`    | `#B8422E` | Terracotta — primary CTA, active state, brand |
| `--accent-2`  | `#D4673B` | Hover/secondary accent |
| `--accent-tint`|`#F4DDCF` | Selected row, accent surfaces |
| `--ok`        | `#3F7C4D` | Success / play state |
| `--warn`      | `#C58A2B` | Caution |
| `--err`       | `#9C3327` | Crash / error |

Maintain ≥ 4.5:1 contrast against `--bg` for body text, ≥ 3:1 for icons.

---

## 3 · Typography Rules

| Level | Family | Weight | Size | Line | Tracking |
|---|---|---|---|---|---|
| Display     | "Tiempos Headline", "Source Serif 4", Georgia, serif | 600 | 28 / 22 | 1.1 | -0.02em |
| Title       | Tiempos Headline, serif | 600 | 17 / 15 | 1.2 | -0.01em |
| Body        | "Inter", "PingFang SC", system-ui, sans-serif | 400 | 14 | 1.55 | 0 |
| Body-Strong | Inter | 600 | 14 | 1.55 | 0 |
| Label       | Inter | 500 | 11 | 1.4 | 0.04em |
| Caption     | Inter | 400 | 10 | 1.4 | 0 |
| Mono / Number | "JetBrains Mono", ui-monospace | 500 | 13 | 1.3 | 0 |

Rule: never mix more than two type families on screen. Numerals in
HUD-like readouts (time, speed, altitude) use Mono.

---

## 4 · Component Stylings

### Buttons
- **Primary**: `--accent` background, white text, 8px radius,
  `padding: 8px 14px`, no gradient, hover lifts to `--accent-2`,
  active settles back; subtle 4% drop shadow.
- **Secondary**: transparent background, 1px `--rule` border, `--ink`
  text. Hover fills `--bg-mute`.
- **Ghost / icon**: transparent, no border, hover `--bg-mute`. Used in
  the camera bar and toolbar.

### Cards / Panels
- White (`--bg-elev`), 1px `--rule` border, 12px radius, `2 8 24 / 0 0 0
  rgba(0,0,0,.04)` two-tier shadow.
- Section headers: serif Title, all caps Label below.

### Inputs / Selects
- 32px tall, 1px `--rule` border, 6px radius, white, `--ink` text. Focus
  ring is 2px `--accent` outer.

### Dropdown / popover
- White surface, `--rule` border, 12px radius, soft shadow
  `0 12 32 rgba(20,20,20,.08)`. Items: 8px padding, hover `--bg-mute`,
  selected `--accent-tint`.

### Comms call menu
- Card on `--bg-elev`, columns separated by 1px `--rule`. Each entry is
  a ghost button + small kbd badge.

### kbd
- `--bg-mute` background, `--rule` border, 4px radius, 9px Mono.

### Timeline
- Track `--bg-mute`, fill `--accent-tint` (current) → `--accent`
  (passed). Marker is a 12×12 circle with `--accent` fill + white border.

---

## 5 · Layout Principles

- **Two-column shell** on desktop: 360px left planner, fluid right
  viewport. On `<= 900px` viewport the planner becomes a slide-in
  drawer triggered by a 40px circular burger button.
- **Vertical rhythm** anchored to 8px grid (8, 16, 24, 32 …).
- The 3D viewport never sleeves under chrome — overlays float with
  10-14px outer margin and respect notch via `env(safe-area-inset-*)`.
- Forms inside the planner are dense (10px row gap) but each row keeps
  16px horizontal padding.

---

## 6 · Depth & Elevation

| Layer | Elevation | Shadow |
|---|---|---|
| Page | 0 | none |
| Planner panel | 1 | `0 1 0 var(--rule)` (right border only on desktop) |
| Card / popover | 2 | `0 2 8 rgba(20,20,20,.04), 0 8 24 rgba(20,20,20,.06)` |
| Drawer (mobile) | 3 | `8 0 30 rgba(0,0,0,.12)` |
| Modal / scrim | 4 | scrim `rgba(20,20,20,.45)` |

No internal shadows on inputs. No dual glows.

---

## 7 · Do's and Don'ts

**Do**
- Keep the 3D viewport untouched — it's the show.
- Use one accent color and one serif family.
- Use whitespace as a design element; let the simulation breathe.
- Anchor primary actions on the right (Play, ▶ 起飞) the way real
  planning tools do.

**Don't**
- Don't add neon glows, scan lines, hexagonal frames, or military HUD
  motifs — that read goes on the in-world HUD, not the chrome.
- Don't add rainbow gradients to chrome buttons.
- Don't mix more than two accents.
- Don't use display fonts at < 14px.

---

## 8 · Responsive Behavior

| Breakpoint | Behaviour |
|---|---|
| `<= 900px` | Planner → drawer (86vw, slide-in left). Camera bar → horizontal scroll strip pinned top. Comms grid → 2 columns. Pinch-zoom disabled (Three.js owns gestures). |
| `<= 600px` | Title hides subtitle. Legend hides. Section heads downsize to 12/10. |
| `>= 1280px` | Planner widens to 380px. Comms grid stays 5 columns. |

iOS safe-area: every fixed element pads `env(safe-area-inset-*)`.
Body height uses `100dvh` so the collapsing toolbar doesn't clip.

---

## 9 · Agent Prompt Guide

When asked to add a new UI element to this project:

1. Read `--bg`, `--ink`, `--accent`, `--rule` from `:root`.
2. Pick the semantically correct component archetype above (button /
   card / dropdown / kbd) and reuse its CSS class. Don't invent new
   shadows or radii.
3. Place primary CTAs on the right; let secondary actions ghost.
4. If text density is high (a list, a log), use Body 14/1.55. If it's
   a HUD readout (numbers), switch to Mono 13.
5. Never overlay 3D viewport content with opaque chrome that blocks
   more than 1/3 of the canvas.
6. Don't introduce a third typography family or a fourth accent.
   Reach for `--accent-2` first.

---

*This document is itself the source of truth for the visual system.
Update it before changing CSS in `index.html`, not after.*
