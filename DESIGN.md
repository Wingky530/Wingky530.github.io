---
version: "2.0"
name: Wingky
description: "A vibe coder who actually gives a damn."
colors:
  charcoal: "#252422"
  charcoal-deep: "#1a1917"
  parchment: "#ebebdf"
  parchment-deep: "#ddddd2"
  arc-blue: "#03a9f4"
  arc-blue-deep: "#0369a1"
  signal-amber: "#f4a903"
  signal-amber-light: "#c78700"
  terminal-green: "#34d399"
  terminal-green-light: "#059669"
  workshop-muted: "#918f89"
  workshop-muted-light: "#5c5b56"
  workshop-border: "#3a3835"
  workshop-border-light: "#d4d2c8"
  bar: "#1a1917"
  bar-light: "#2f2d2a"
typography:
  display:
    fontFamily: "Wingky, sans-serif"
    fontSize: "clamp(4rem, 10vw, 6rem)"
    fontWeight: 900
    lineHeight: 1
    letterSpacing: "0.05em"
  body:
    fontFamily: "Wingky, sans-serif"
    fontSize: "1rem"
    fontWeight: 400
    lineHeight: "1.625"
  label:
    fontFamily: "Wingky, sans-serif"
    fontSize: "0.65rem"
    fontWeight: 500
    letterSpacing: "0.22em"
    textTransform: "uppercase"
rounded:
  sm: "4px"
  md: "8px"
  lg: "12px"
  full: "9999px"
components:
  nav-bar:
    backgroundColor: "{colors.bar}"
    height: "56px"
    position: "sticky top-0"
    zIndex: 50
  footer-bar:
    backgroundColor: "{colors.bar}"
    height: "40px"
    zIndex: 40
  tri-stripe:
    height: "3px"
    colors: ["{colors.arc-blue}", "{colors.signal-amber}", "{colors.terminal-green}"]
  dossier-panel:
    border: "1px solid {colors.workshop-border}"
    rounded: "{rounded.md}"
    headerBg: "{colors.bar}"
  theme-toggle:
    backgroundColor: "{colors.bar}"
    border: "1px solid {colors.workshop-border}"
    rounded: "{rounded.full}"
    hoverBorder: "{colors.signal-amber}"
---

# Design System: Wingky (Endfield Edition)

## 1. Overview

**Creative North Star: "The Command Center"**

Inspired by Arknights: Endfield's industrial sci-fi UI — dark bars, tri-color accent stripes, topographic contour textures, and panel-based layouts. The portfolio feels like an operator terminal: precise, layered, and purposeful.

The system retains the original Wingky palette warmth (Charcoal + Parchment) while adding Endfield's structural language: dark bar headers/footers, tri-color stripe separators, contour-map backgrounds, and panel containers with status indicators.

**Key Characteristics:**

- Dark bars at top/bottom — solid dark surfaces that frame content
- Tri-color accent stripe (Arc Blue / Signal Amber / Terminal Green) as separator
- Topographic contour-map SVG as subtle full-page texture
- Panel-based content containers with dark bar headers
- Radial gradient background (center → edges) for depth
- Tech-readout labels and status indicators
- Single custom font (Wingky) — weight-based hierarchy only

## 2. Colors

### Primary Accent

- **Arc Blue** (`#03a9f4` dark / `#01517a` light): Primary accent for interactive elements, the title dot, CTA buttons.

### Signal Accents (Endfield Tri-Stripe)

- **Signal Amber** (`#f4a903` dark / `#c78700` light): Used in tri-stripe, section labels, nav link highlights, panel header text.
- **Terminal Green** (`#34d399` dark / `#059669` light): Used in tri-stripe, status indicators ("● Active", "● ONLINE"), protocol labels.

### Neutral

- **Charcoal** (`#252422`): Primary background surface (dark mode).
- **Charcoal Deep** (`#1a1917`): Radial gradient endpoint, dark bar surface.
- **Parchment** (`#ebebdf`): Light mode background, dark mode text.
- **Workshop Muted** (`#918f89` dark / `#5c5b56` light): Secondary text, labels.
- **Workshop Border** (`#3a3835` dark / `#d4d2c8` light): Panel borders, dividers.

### Named Rules

**Tri-Color Rule.** The three accents have distinct roles — Blue = interactive, Amber = labels/navigation, Green = status/protocol. They appear together only in the TriStripe component.

**Dark Bar Rule.** All bars (nav, footer, panel headers) use `--color-bar` — a near-black surface darker than the page background. Text inside bars is always `--color-primary` or an accent.

## 3. Components

### TriStripe

A 3px-high bar split into three equal color segments (Arc Blue / Signal Amber / Terminal Green) via CSS linear-gradient. Used as separator between dark bars and content.

- **Height:** 3px default, 2px for panel separators
- **Orientation:** Horizontal (default) or vertical
- **Placement:** Below nav bar, above footer bar, between panel-header and panel-content

### TopoBackground

Fixed full-viewport SVG with organic contour-map lines at 6% opacity. Uses `--color-border` for stroke color so it adapts to theme automatically. Multiple ring clusters at various positions for depth.

- **Z-index:** 0 (below all content)
- **Opacity:** 0.06 default
- **Interaction:** None (pointer-events: none, aria-hidden)

### Nav (Dark Bar Header)

Sticky dark bar at top with AnimatedTitle left, nav links/menu toggle right. TriStripe below.

- **Background:** `--color-bar`
- **Height:** 56px
- **Links:** Signal Amber accent color, uppercase, tracked
- **Hamburger:** Second bar in amber accent
- **Z-index:** 50

### Footer (Dark Bar Footer)

Static bottom bar with TriStripe above. "wingky" brand text left, © year right.

- **Background:** `--color-bar`
- **Height:** 40px
- **Text:** Workshop Muted, 0.75rem
- **Z-index:** 40

### Dossier Panel

Bordered container for content sections. Dark bar header + TriStripe + content body.

- **Border:** 1px workshop-border, 8px radius
- **Header:** `--color-bar` bg, amber label text (0.65rem, tracked, uppercase)
- **Separator:** TriStripe at 2px height
- **Content:** 20px padding

### Theme Toggle

Fixed bottom-center (above footer). Black hole icon retained. Dark bar background with workshop-border stroke.

- **Background:** `--color-bar`
- **Border:** 1px workshop-border → amber on hover
- **Position:** fixed, bottom 56px (clears footer)
- **Mechanics:** Same clip-path reveal, same grid ripple dispatch

## 4. Page Layouts

### Landing (Command Center)

- Fixed dark bar at top: "Protocol Field Recovery" label + green "● ONLINE" status
- TriStripe below bar
- Centered AnimatedTitle with stroke-draw animation
- Nav links in amber accent
- Tagline below title
- TopoBackground + radial gradient visible

### Projects (Assignment Briefing)

- Sticky Nav bar
- Section header: amber "Assignment Briefing" label + rule line + page title
- Each project in a `.project-panel`: dark bar header (green status + project name) → TriStripe → content
- Max-width 6xl, centered

### About (Operator Dossier)

- Sticky Nav bar
- Hero: amber "Operator Dossier" label + green "● Active" status + AnimatedTitle
- Sections as `.dossier-panel`: Field Data, Operating Protocol, Mission Log, Equipment Loadout, Comms Channel
- Precision statement as standalone block (no panel)
- Tech badges with hover-fill interaction retained

## 5. Typography

Same as v1 — single Wingky font family, weight-based hierarchy (900 display, 700 heading, 400 body, 500 label). No second typeface.

Label style updated: 0.65rem (from 0.75rem), tracking 0.22em, uppercase. Used for panel headers and status indicators.

## 6. Background System

- **Radial gradient:** `radial-gradient(ellipse at center, --color-background 0%, --color-background-end 100%)`
- **Topographic SVG:** Fixed full-viewport, 6% opacity contour lines
- **Combined effect:** Subtle depth without violating flat-surface philosophy — no shadows, no blur

## 7. Responsive Behavior

Same two-tier system (mobile + md:768px+). Dark bars scale with viewport. Panels go full-width on mobile with maintained padding. Nav uses hamburger on mobile, inline links on desktop.

## 8. Known Gaps

- TopoBackground SVG paths are static — no randomization or animation
- Tri-stripe does not animate (intentional — it's a structural element)
- Light mode `--color-bar` uses a dark surface (#2f2d2a) for contrast — bars stay dark in both themes
- Panel layout on projects page may need adjustment if project components have their own padding
