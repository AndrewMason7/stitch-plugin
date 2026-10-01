---
version: alpha
name: Taste Standard
description: High-agency, anti-slop design system for Google Stitch with calibrated color, distinctive typography, and spring motion physics.
colors:
  primary: '#047857'
  on-primary: '#FFFFFF'
  background: '#F9FAFB'
  on-background: '#18181B'
  surface: '#FFFFFF'
  on-surface: '#18181B'
  secondary: '#71717A'
  on-secondary: '#FFFFFF'
  muted: '#94A3B8'
  outline: 'rgba(226, 232, 240, 0.5)'
typography:
  display:
    fontFamily: Geist
    fontSize: 48px
    fontWeight: '800'
    lineHeight: 1.1
    letterSpacing: -0.025em
  body:
    fontFamily: Geist
    fontSize: 16px
    fontWeight: '400'
    lineHeight: 1.65
    letterSpacing: 0px
  mono:
    fontFamily: Geist Mono
    fontSize: 13px
    fontWeight: '500'
    lineHeight: 1.4
    letterSpacing: 0px
rounded:
  sm: 4px
  md: 8px
  lg: 16px
  card: 40px
  full: 9999px
spacing:
  base: 16px
  xs: 4px
  sm: 8px
  md: 16px
  lg: 24px
  xl: 32px
  container: 1400px
components:
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.on-primary}"
    rounded: "{rounded.md}"
    padding: 12px
  button-secondary:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    rounded: "{rounded.md}"
    padding: 12px
  badge:
    backgroundColor: "{colors.muted}"
    textColor: "{colors.on-surface}"
    rounded: "{rounded.full}"
    padding: 4px
  card:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    rounded: "{rounded.lg}"
    padding: 24px
---

# Design System: Taste Standard

## Overview

A restrained, gallery-airy interface with confident asymmetric layouts and fluid spring-physics motion. The atmosphere is clinical yet warm — like a well-lit architecture studio where every element earns its place through function. Density is balanced (Level 5), variance runs high (Level 8) to prevent symmetrical boredom, and motion is fluid but never theatrical (Level 6). The overall impression: expensive, intentional, alive.

### Configuration Dials
- **Creativity**: `9` (Inline image typography, dramatic scale contrast, high editorial flow)
- **Density**: `5` (Balanced whitespace)
- **Variance**: `8` (Asymmetric layouts, no two sections alike)
- **Motion Intent**: `6` (Fluid spring physics on interactive components)

## Colors

The palette is rooted in high-contrast neutral foundations and a single calibrated accent color.

- **Primary (#047857):** "Emerald Signal" — the sole interactive accent color driver for growth, conversion, and primary actions.
- **Background (#F9FAFB):** "Canvas White" — warm-neutral primary background surface, never clinical blue-white.
- **Surface (#FFFFFF):** "Pure Surface" — card and container fill used with whisper shadow for elevation.
- **On-Surface (#18181B):** "Charcoal Ink" — primary typography and headings (Zinc-950 depth, never pure black).
- **Secondary (#71717A):** "Steel Secondary" — body copy, descriptions, and supporting metadata.
- **Muted (#94A3B8):** "Muted Slate" — timestamps, tertiary labels, and inactive icon states.

## Typography

Typography establishes an institutional, modern, and trustworthy voice through **Geist** and **Geist Mono**.

- **Display Headlines:** Set in Geist Bold/Black (700–900 weight) with tight tracking (`-0.025em`) and compressed leading (`1.1`). Scale scales down gracefully via `clamp(2.25rem, 5vw, 3.75rem)` in CSS.
- **Body Copy:** Set in Geist Regular at 16px with relaxed leading (1.65) and a strict 65-character maximum line length for optimal readability.
- **Monospace Metadata:** Set in Geist Mono at 13px for data tables, timestamps, code snippets, and metric counters.

## Layout

The layout is built on CSS Grid architecture with strict responsive containment.

- **Grid-First:** CSS Grid is used for all structural layouts. Percentage math hacks (`calc(33% - 1rem)`) are banned.
- **Containment:** All content is bounded within a centered max-width of 1400px with responsive horizontal padding (`clamp(1rem, 4vw, 4rem)`).
- **Hero Section:** Features asymmetric layout and inline image typography where small contextual photos sit inline at type-height as visual punctuation. Centered heroes are banned.
- **Full-Height Sections:** Always use `min-height: 100dvh` — never `height: 100vh` to avoid iOS Safari address bar jumps.

## Elevation & Depth

Depth is conveyed through tonal layers and wide, diffused ambient shadows rather than harsh drop shadows.

- **Surface Elevation:** Background elements rest at the canvas layer. Elevated cards utilize Pure Surface (#FFFFFF) with a 1px whisper border (`rgba(226, 232, 240, 0.5)`) and a subtle 40px diffused shadow (`0 20px 40px -15px rgba(0, 0, 0, 0.05)`).
- **Floating Modals:** Top-tier floating elements feature soft ambient elevation with backdrop blur (`backdrop-blur-md`).

## Shapes

The shape language pairs disciplined structure with tactile, approachable roundness.

- **Cards & Panels:** Generous 40px (`2.5rem`) corner radius on major containers.
- **Interactive Elements:** Buttons, inputs, and chips feature 8px corner radii (`rounded-md`).
- **Pills & Badges:** Full 9999px roundness for status chips and notification pills.

## Components

- **Buttons:** Tactile feedback on active states (`transform: scale(0.98)`). Primary buttons use Emerald Signal fill with white text. Ghost/outline buttons use 1px outline with hover background shift. Outer glows and neon button borders are banned.
- **Cards:** Used strictly when elevation communicates hierarchy. In high-density views, cards are replaced by 1px border dividers or whitespace.
- **Inputs:** Labels positioned strictly above fields; error text below in high contrast. Focus rings feature 2px offset in the primary accent hue.
- **Loading States:** Skeletal shimmer loaders matching component geometries. Circular loading spinners are banned.

## Do's and Don'ts

- Do use exactly one primary accent color per application surface.
- Do replace all `href="#"` placeholders with authentic routing links during code export.
- Do enforce minimum 44px tap targets for mobile interactive elements.
- Don't use pure black (`#000000`) for text or backgrounds — use Zinc-950 or Charcoal Ink.
- Don't use the generic 3-equal-cards feature row — use asymmetric Bento grids or 2-column Zig-Zag.
- Don't invent fake AI metrics or statistics ("99.99% Uptime", "124ms Latency") — use real data or `[metric]` placeholders.
- Don't use emojis anywhere in the interface or code.
