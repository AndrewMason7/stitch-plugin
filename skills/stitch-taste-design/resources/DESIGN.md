---
version: alpha
name: Taste Standard
description: High-agency, anti-slop design system for Google Stitch enforcing calibrated color, distinctive typography, asymmetric layouts, and spring motion physics.
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
    fontSize: 3.75rem
    fontWeight: '800'
    lineHeight: 1.1
    letterSpacing: -0.025em
  body:
    fontFamily: Geist
    fontSize: 1rem
    fontWeight: '400'
    lineHeight: 1.65
    letterSpacing: 0em
  mono:
    fontFamily: Geist Mono
    fontSize: 0.8125rem
    fontWeight: '500'
    lineHeight: 1.4
    letterSpacing: 0em
rounded:
  sm: 4px
  md: 8px
  lg: 16px
  card: 40px
  full: 9999px
spacing:
  xs: 4px
  sm: 8px
  md: 16px
  lg: 24px
  xl: 32px
  2xl: 40px
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
    rounded: "{rounded.card}"
    padding: 32px
---

# Design System: Taste Standard
**Skill:** stitch-taste-design

---

## Overview

A restrained, gallery-airy interface with confident asymmetric layouts and fluid spring-physics motion. The atmosphere is clinical yet warm — like a well-lit architecture studio where every element earns its place through function. Density is balanced (Level 5), variance runs high (Level 8) to prevent symmetrical boredom, and motion is fluid but never theatrical (Level 6). The overall impression: expensive, intentional, alive.

### Configuration — Set Your Style
Adjust these dials before using this design system. They control how creative, dense, and animated the output should be. Pick the level that fits your project.

| Dial | Level | Description |
|------|-------|-------------|
| **Creativity** | `9` | `1` = Ultra-minimal, Swiss, silent, monochrome. `5` = Balanced, clean but with personality. `10` = Expressive, editorial, bold typography experiments, inline images in headlines, strong asymmetry. Default: `9` |
| **Density** | `5` | `1` = Gallery-airy, massive whitespace. `5` = Balanced sections. `10` = Cockpit-dense, data-heavy. Default: `5` |
| **Variance** | `8` | `1` = Predictable, symmetric grids. `5` = Subtle offsets. `10` = Artsy chaotic, no two sections alike. Default: `8` |
| **Motion Intent** | `6` | `1` = Static, no animation noted. `5` = Subtle hover/entrance cues. `10` = Cinematic orchestration noted in every component. Default: `6` |

> **How to use:** Change the numbers above to match your project's vibe. At **Creativity 1–3**, the system produces clean, quiet, Notion-like interfaces. At **Creativity 7–10**, expect inline image typography, dramatic scale contrast, and strong editorial layouts. The rest of the rules below adapt to your chosen levels.

## Colors
- **Canvas White** (#F9FAFB) — Primary background surface. Warm-neutral, never clinical blue-white
- **Pure Surface** (#FFFFFF) — Card and container fill. Used with whisper shadow for elevation
- **Charcoal Ink** (#18181B) — Primary text. Zinc-950 depth — never pure black
- **Steel Secondary** (#71717A) — Body text, descriptions, metadata. Zinc-500 warmth
- **Muted Slate** (#94A3B8) — Tertiary text, timestamps, disabled states
- **Whisper Border** (rgba(226,232,240,0.5)) — Card borders, structural 1px lines. Semi-transparent for depth
- **Diffused Shadow** (rgba(0,0,0,0.05)) — Card elevation. Wide-spreading, 40px blur, -15px offset. Never harsh

### Accent Selection (Pick ONE per project — WCAG AA Compliant >= 4.5:1 with White Text)
- **Emerald Signal** (#047857) — For growth, success, positive data dashboards
- **Electric Blue** (#1D4ED8) — For productivity, SaaS, developer tools
- **Deep Rose** (#BE123C) — For creative, editorial, fashion-adjacent projects
- **Amber Warmth** (#B45309) — For community, social, warm-toned products

### Banned Colors
- Purple/Violet neon gradients — the "AI Purple" aesthetic
- Pure Black (#000000) — always Off-Black or Zinc-950
- Oversaturated accents above 80% saturation
- Mixed warm/cool gray systems within one project

## Typography
- **Display:** `Geist`, `Satoshi`, `Cabinet Grotesk`, or `Outfit` — Track-tight (`-0.025em`), controlled fluid scale, weight-driven hierarchy (700–900). Not screaming. Leading compressed (`1.1`). Alternatives forced — `Inter` is BANNED for premium contexts
- **Body:** Same family at weight 400 — Relaxed leading (`1.65`), 65ch max-width, Steel Secondary color (#71717A)
- **Mono:** `Geist Mono` or `JetBrains Mono` — For code blocks, metadata, timestamps. When density exceeds Level 7, all numbers switch to monospace
- **Scale:** Display at `clamp(2.25rem, 5vw, 3.75rem)`. Body at `1rem/1.125rem`. Mono metadata at `0.8125rem`

### Banned Fonts
- `Inter` — banned everywhere in premium/creative contexts
- Generic serif fonts (`Times New Roman`, `Georgia`, `Garamond`, `Palatino`) — BANNED. If serif is needed for editorial/creative, use only distinctive modern serifs like `Fraunces`, `Gambarino`, `Editorial New`, or `Instrument Serif`. Never use default browser serif stacks. Serif is always BANNED in dashboards or software UIs regardless

## Layout
- **Grid-First:** CSS Grid for all structural layouts. Never flexbox percentage math (`calc(33% - 1rem)` is BANNED)
- **No Overlapping:** Elements must never overlap each other. No absolute-positioned layers stacking content on content. Every element occupies its own grid cell or flow position. Clean, separated spatial zones
- **Feature Sections:** The "3 equal cards in a row" pattern is BANNED. Use 2-column Zig-Zag, asymmetric Bento grids (2fr 1fr 1fr), or horizontal scroll galleries
- **Containment:** All content within `max-width: 1400px`, centered. Generous horizontal padding (`1rem` mobile, `2rem` tablet, `4rem` desktop)
- **Full-Height:** Use `min-height: 100dvh` — never `height: 100vh` (iOS Safari address bar jump)
- **Bento Architecture:** For feature grids, use Row 1: 3 columns | Row 2: 2 columns (70/30 split). Each tile contains a perpetual micro-animation

### Hero Section
The Hero is the first impression — it must be striking, creative, and never generic.
- **Inline Image Typography:** Embed small, contextual photos or visuals directly between words or letters in the headline. Example: "We build [photo of hands typing] digital [photo of screen] products" — images sit inline at type-height, rounded, acting as visual punctuation between words. This is the signature creative technique
- **No Overlapping Elements:** Text must never overlap images or other text. Every element has its own clear spatial zone. No z-index stacking of content layers, no absolute-positioned headlines over images. Clean separation always
- **No Filler Text:** "Scroll to explore", "Swipe down", scroll arrow icons, bouncing chevrons, and any instructional UI chrome are BANNED. The user knows how to scroll. Let the content pull them in naturally
- **Asymmetric Structure:** Centered Hero layouts are BANNED at this variance level. Use Split Screen (50/50), Left-Aligned text / Right visual, or Asymmetric Whitespace with large empty zones
- **CTA Restraint:** Maximum one primary CTA button. No secondary "Learn more" links. No redundant micro-copy below the headline

### Responsive Rules
Every screen must work flawlessly across all viewports. **Responsive is not optional — it is a hard requirement. Every single element must be tested at 375px, 768px, and 1440px.**
- **Mobile-First Collapse (< 768px):** All multi-column layouts collapse to a strict single column. `width: 100%`, `padding: 1rem`, `gap: 1.5rem`. No exceptions
- **No Horizontal Scroll:** Horizontal overflow on mobile is a critical failure. All elements must fit within viewport width. If any element causes horizontal scroll, the design is broken
- **Typography Scaling:** Headlines scale down gracefully via `clamp()`. Body text stays `1rem` minimum. Never shrink body below `14px`. Headlines must remain readable on 375px screens
- **Touch Targets:** All interactive elements minimum `44px` tap target. Generous spacing between clickable items. Buttons must be full-width on mobile
- **Image Behavior:** Hero and inline images scale proportionally. Inline typography images (photos between words) stack below the headline on mobile instead of inline
- **Navigation:** Desktop horizontal nav collapses to a clean mobile menu (slide-in or full-screen overlay). No tiny hamburger icons without labels
- **Cards & Grids:** Bento grids and asymmetric layouts revert to stacked single-column cards with full-width. Maintain internal padding (`1rem`)
- **Spacing Consistency:** Vertical section gaps reduce proportionally on mobile (`clamp(3rem, 8vw, 6rem)`). Never cramped, never excessively airy
- **Testing Viewports:** Designs must be verified at: `375px` (iPhone SE), `390px` (iPhone 14), `768px` (iPad), `1024px` (small laptop), `1440px` (desktop)

## Elevation & Depth
- **Tonal Layering:** Canvas White (`#F9FAFB`) background paired with Pure Surface (`#FFFFFF`) elevated cards.
- **Whisper Borders & Diffused Shadows:** 1px semi-transparent borders (`rgba(226,232,240,0.5)`) and wide-spreading diffused shadows (`0 20px 40px -15px rgba(0,0,0,0.05)`). Harsh drop shadows and neon outer glows are strictly banned.

## Shapes
- **Cards & Containers:** Generous `2.5rem` (`40px`) corner radius on elevated cards.
- **Interactive Controls:** Tactile `8px` (`rounded-md`) corner radius on buttons and inputs.
- **Badges & Pills:** Full `9999px` pill geometry for status indicators and chips.

## Components
* **Buttons:** Flat surface, no outer glow. Primary: accent fill with white text. Secondary: ghost/outline. Active state: `-1px translateY` or `scale(0.98)` for tactile push. Hover: subtle background shift, never glow
* **Cards/Containers:** Generously rounded corners (`2.5rem`). Pure white fill. Whisper border (`1px`, semi-transparent). Diffused shadow (`0 20px 40px -15px rgba(0,0,0,0.05)`). Internal padding `2rem–2.5rem`. Used ONLY when elevation communicates hierarchy — high-density layouts replace cards with `border-top` dividers or negative space
* **Inputs/Forms:** Label positioned above input. Helper text optional. Error text below in Deep Rose. Focus ring in accent color, `2px` offset. No floating labels. Standard `0.5rem` gap between label-input-error stack
* **Navigation:** Sleek, sticky. Icons scale on hover (Dock Magnification optional). No hamburger on desktop. Clean horizontal with generous spacing
* **Loaders:** Skeletal shimmer matching exact layout dimensions and rounded corners. Shifting light reflection across placeholder shapes. Never circular spinners
* **Empty States:** Composed illustration or icon composition with guidance text. Never just "No data found"
* **Error States:** Inline, contextual. Red accent underline or border. Clear recovery action

### Motion & Interaction (Code-Phase Intent)
> **Note:** Stitch generates static screens — it does not animate. This section documents the **intended motion behavior** so that the coding agent (Antigravity, Cursor, etc.) knows exactly how to implement animations when building the exported design into a live product.

- **Physics Engine:** Spring-based exclusively. `stiffness: 100, damping: 20`. No linear easing anywhere. Premium, weighty feel on all interactive elements
- **Perpetual Micro-Loops:** Every active dashboard component has an infinite-loop state — Pulse on status dots, Typewriter on search bars, Float on feature icons, Shimmer on loading states
- **Staggered Orchestration:** Lists and grids mount with cascaded delays (`animation-delay: calc(var(--index) * 100ms)`). Waterfall reveals, never instant mount
- **Layout Transitions:** Smooth re-ordering via shared element IDs. Items swap positions with physics, simulating real-time intelligence
- **Hardware Rules:** Animate ONLY `transform` and `opacity`. Never `top`, `left`, `width`, `height`. Grain/noise filters on fixed, pointer-events-none pseudo-elements only
- **Performance:** CPU-heavy perpetual animations isolated in microscopic leaf components. Never trigger parent re-renders. Target 60fps minimum

## Do's and Don'ts
- Do use a single primary accent color per project surface with saturation below 80%.
- Do enforce minimum 44px touch targets and test layouts at 375px, 768px, and 1440px.
- Don't use emojis — anywhere in UI, code, or alt text
- Don't use `Inter` font — use `Geist`, `Outfit`, `Cabinet Grotesk`, `Satoshi`
- Don't use generic serif fonts (`Times New Roman`, `Georgia`, `Garamond`) — if serif is needed, use distinctive modern serifs only (`Fraunces`, `Instrument Serif`)
- Don't use pure black (`#000000`) — Off-Black or Zinc-950 only
- Don't use neon outer glows or default box-shadow glows
- Don't use oversaturated accent colors above 80%
- Don't use excessive gradient text on large headers
- Don't use custom mouse cursors
- Don't overlap elements — text never overlaps images or other content. Clean spatial separation always
- Don't use 3-column equal card layouts for features
- Don't use centered Hero sections (at this variance level)
- Don't use filler UI text: "Scroll to explore", "Swipe down", "Discover more below", scroll arrows, bouncing chevrons — all BANNED
- Don't use generic names: "John Doe", "Sarah Chan", "Acme", "Nexus", "SmartFlow"
- Don't use fake round numbers: `99.99%`, `50%`, `1234567` — use organic data: `47.2%`, `+1 (312) 847-1928`
- Don't fabricate data or statistics — never generate metrics, performance numbers, uptime percentages, response times, or any data not explicitly provided by the user. "99.98% UPTIME SLA", "124ms AVG. RESPONSE", "18.5k DEPLOY CYCLES" are invented AI filler. Use `[metric]` placeholders if real data is unavailable
- Don't create fake system/metric sections — "SYSTEM PERFORMANCE METRICS", "KEY STATISTICS", "BY THE NUMBERS" dashboard cards filled with invented data are BANNED
- Don't use `LABEL // YEAR` formatting — "SYSTEM // 2024", "METRICS // 2025" is a lazy AI convention, not real design typography
- Don't use AI copywriting clichés: "Elevate", "Seamless", "Unleash", "Next-Gen", "Revolutionize"
- Don't use broken Unsplash links — use `picsum.photos/seed/{id}/800/600` or SVG UI Avatars
- Don't use generic `shadcn/ui` defaults — customize radii, colors, shadows to match this system
- Don't spam `z-index` — use only for Navbar, Modal, Overlay layer contexts
- Don't use `h-screen` — always `min-h-[100dvh]`
- Don't use circular loading spinners — skeletal shimmer only
