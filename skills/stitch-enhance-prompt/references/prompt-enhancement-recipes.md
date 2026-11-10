# Stitch Prompt Enhancement Recipes

High-performing structural prompt templates engineered for the Google Stitch screen generation pipeline.

> [!NOTE]
> **Design System Separation:** In accordance with Stitch prompt architecture, these generation recipes focus strictly on **layout, component hierarchy, and interactive structure**. Color palettes, typography tokens, and corner roundness should be managed at the project level via `.stitch/DESIGN.md` and passed through the `designSystem` parameter rather than hardcoded into generation prompts.

---

## 1. SaaS Executive Dashboard (Desktop, 1280px)

```text
A modern B2B SaaS executive metrics dashboard with elevated glassmorphic surfaces and asymmetric Bento grid organization.

**PLATFORM:** Web, Desktop-first (1280px max-width container)

**PAGE STRUCTURE:**
1. **Left Navigation Sidebar:** Fixed vertical navigation rail with brand mark at top, primary workspace links (Overview, Revenue, Cohorts, Settings) with active indicator bar, and collapsed icon mode toggle at bottom.
2. **Sticky Top Header:** Breadcrumb trail on the left, global command-palette search input (`Cmd+K` badge) in the center, and notification bell + user profile trigger on the right.
3. **KPI Summary Row:** 4-column metric strip (ARR, Net Dollar Retention, Active Workspaces, Churn Rate), each card containing a primary monospace metric readout, period-over-period delta badge, and inline micro-sparkline.
4. **Asymmetric Analytics Bento Grid:**
   - **Primary Tile (Left 65%):** Interactive multi-series area chart for revenue trajectory with timeframe segmented controls (7D, 30D, QTD, YTD).
   - **Secondary Tile (Right 35%):** Live customer activity feed with status pills, workspace avatars, and relative timestamps.
5. **High-Density Transactions Table:** Filterable data table with sticky column headers, sortable numeric columns, status chips (Settled, Pending, Flagged), and pagination controls.
```

---

## 2. Crypto Portfolio & DeFi Tracker (Mobile, 390px)

```text
A tactile mobile portfolio and asset tracking interface designed for one-handed thumb navigation and rapid financial scanning.

**PLATFORM:** Mobile, Portrait (390px viewport, 44px minimum touch targets)

**PAGE STRUCTURE:**
1. **Top App Bar:** Compact header featuring network status indicator pill on the left, truncated wallet address chip with copy trigger in the center, and QR scanner action button on the right.
2. **Portfolio Balance Hero:** Asymmetric left-aligned balance readout in large display scale with 24-hour delta pill, paired with an interactive scrubbing sparkline and timeframe selector tabs (1H, 1D, 1W, 1M, ALL).
3. **Quick Action Dock:** 4-button tactile action row (Send, Receive, Swap, Bridge) with distinct icon containers and concise labels.
4. **Holdings List Section:** Section header with sort filter ("By Value"), followed by a vertical stack of asset rows showing token emblem, name, ticker symbol, current balance, fiat valuation, and 24h percentage change.
5. **Bottom Navigation Bar:** Fixed 4-tab bar (Portfolio, Markets, Activity, Settings) with frosted backdrop blur and active tab indicator.
```

---

## 3. Developer Platform Landing Page (Desktop, 1280px)

```text
An editorial, high-contrast developer platform landing page featuring an asymmetric split-screen hero and modular Bento feature showcase.

**PLATFORM:** Web, Desktop-first (1280px responsive grid)

**PAGE STRUCTURE:**
1. **Sticky Header:** Horizontal navigation bar with brand mark on the left, section links (Architecture, SDK, Benchmarks, Docs, Pricing) in the center, and a single primary CTA button ("Start Building") on the right.
2. **Asymmetric Split Hero (60/40):**
   - **Left Column:** Category eyebrow badge, high-contrast display headline with inline visual punctuation, concise 65ch technical value proposition, and a primary action form (email input + submit CTA) paired with a copyable CLI install snippet.
   - **Right Column:** Interactive multi-tab code editor and terminal preview window demonstrating live SDK initialization and streaming telemetry output.
3. **Asymmetric Feature Bento Grid (2-Row):**
   - **Row 1 (65/35 Split):** Architecture diagram card showcasing zero-latency edge routing alongside a real-time benchmark comparison card.
   - **Row 2 (35/65 Split):** Security and compliance specification card paired with an interactive API schema explorer preview.
4. **Footer:** Structured 4-column documentation and resource directory, system status indicator pill, and copyright metadata.
```
