# Google Stitch UI/UX Engineering & Design-to-Code Protocol

When interacting with Google Stitch, designing UI components, or converting Stitch designs into production code:

---

## 1. Tool Priority & MCP Integration
- **Always Prefer Dedicated Stitch MCP Tools**: Use `call_mcp_tool(ServerName: "stitch", ToolName: "...")` for all design generation, project management, and variant generation tasks.
  - Project Management: `create_project`, `list_projects`, `get_project`, `delete_project`.
  - Screen Generation & Variants: `generate_screen_from_text`, `edit_screens`, `generate_variants`, `list_screens`, `get_screen`.
  - Design Systems: `upload_design_md`, `create_design_system_from_design_md`, `create_design_system`, `update_design_system`, `list_design_systems`, `apply_design_system`.
- **Always Skills First**: Proactively consult the 17 bundled skills in `skills/stitch-<name>/SKILL.md` via `view_file` before executing manual procedures.
- **Mandatory Custom Agent Delegation**: For large design refactors, multi-screen mockups, or full application builds, use the specialized `stitch-designer` custom agent.

---

## 2. Mandatory Prompt Enhancement Pipeline
- **Never Submit Raw User Prompts**: Direct model requests like *"make a crypto dashboard"* or *"build a landing page"* produce generic output. You **MUST** enhance prompts with:
  - **Component Structure**: Specify explicit layout blocks (e.g. `TopAppBar`, `StickyFilterBar`, `BentoGrid`, `StatCardsWithSparklines`, `InfiniteScrollTable`).
  - **Spatial Hierarchy & Density**: Define asymmetric splits, grid proportions, and interactive states (`hover`, `active`, `empty`, `loading`).
  - **Separation of Concerns (No Theme Leakage)**: Keep structural layout and component hierarchy in the generation prompt; handle colors, fonts, and corner roundness at the project level via `DESIGN.md` and the Stitch design system tools (hex codes are only permitted in targeted `edit_screens` prompts).
  - **Viewport**: Mobile-first portrait (`deviceType: "MOBILE"`, `390px`) or expansive desktop (`deviceType: "DESKTOP"`, `1280px`).

---

## 3. Design System Alignment (`DESIGN.md`)
- **Semantic Token Discipline**: Always extract and maintain a `DESIGN.md` in the project root.
- **Never Hardcode Arbitrary Hex Values**: Map raw hex values to CSS custom properties or Tailwind semantic tokens (`--color-primary`, `--color-surface`, `--color-text-muted`).
- **Token Validation**: Validate syntax and WCAG AA contrast with `design.md lint DESIGN.md`.
- **Cloud Synchronization**: Synchronize local `DESIGN.md` tokens with the Stitch cloud project using the 3-step sequence: `upload_design_md` (base64) → `create_design_system_from_design_md` → `apply_design_system`.

---

## 4. Production Code Conversion Standards
When converting Stitch generated HTML/CSS into React, Vite, or React Native components:
- **Dead Link Remediation**: Stitch HTML places placeholder `href="#"` attributes on links. Replace every single one with authentic routing (`<Link to="...">` or `<NavLink>`).
- **Responsive Navigation Parity**: Stitch bottom bars typically include `md:hidden`, rendering them invisible on desktop screens. Always provide a fallback desktop header navigation and ensure the brand logo in the `TopAppBar` links back to `/`.
- **Component Decomposition**: Break massive monolithic screens into modular atomic components (`Header`, `Hero`, `FeatureGrid`, `PricingCard`, `Footer`).
- **Accessible State Handling**: Ensure proper empty, loading, and error states for all interactive data views.

---

## 5. Security & Secret Hygiene
- **Zero Committed Secrets**: Never write, log, or commit Stitch API keys into repository files or git history.
- **Environment Variable Resolution**: Always rely on `${STITCH_API_KEY}` runtime configuration provided in `mcp_config.json`.
