---
name: stitch
description: Creates a new Google Stitch project, initializes its design system foundation, and bootstraps initial UI mockups. Triggered by /stitch or user requests to start a new Stitch project.
---

# Stitch Project Creation & Initialization Protocol

Use this skill whenever the user invokes the `/stitch` command or asks to create, initialize, or kick off a new Google Stitch project.

---

## Overview

A Stitch project is a cloud-hosted workspace container (`projects/{projectId}`) that houses UI screen mockups, variant histories, uploaded assets, and semantic design systems.

This skill governs the complete project initialization sequence:
1. Determining and naming the project.
2. Creating the project container via `create_project`.
3. Establishing the project's design token foundation (`DESIGN.md`).
4. Generating the initial screen mockup (`generate_screen_from_text`).
5. Guiding the user toward iterative refinement, variants, and code export.

---

## 4-Step Project Creation Workflow

### Step 1: Clarify Project Intent & Title

1. Extract or deduce a concise, descriptive project title from the user's prompt:
   - User input: `/stitch Modern fintech crypto wallet for iOS`
   - Inferred title: `"Fintech Crypto Wallet"`
2. If the user invokes `/stitch` without arguments, prompt for the product concept or propose a default name based on the workspace.
3. Identify target device viewport:
   - **Mobile** (`deviceType: "MOBILE"`): 390px portrait mobile apps.
   - **Desktop** (`deviceType: "DESKTOP"`): 1280px responsive desktop web apps.

---

### Step 2: Initialize Project Container (`create_project`)

1. Call the `create_project` MCP tool:
   ```json
   {
     "title": "<Project Title>"
   }
   ```
2. Parse the returned resource payload:
   ```json
   {
     "name": "projects/8486754918478854804",
     "title": "Fintech Crypto Wallet",
     "visibility": "PRIVATE",
     "projectType": "PROJECT_DESIGN",
     "origin": "STITCH"
   }
   ```
3. Extract the numeric `projectId` from the `name` field (e.g. `8486754918478854804`). Save this ID in working memory — all subsequent screen generation, variant creation, and design system tools require this exact `projectId`.

---

### Step 3: Establish the Design System (`DESIGN.md`)

Every high-quality Stitch project should be paired with a calibrated semantic design token system:

1. **Workspace Check**: Check whether a `DESIGN.md` file exists in the current project root.
2. **Scaffold Tokens**: If none exists, copy the standard template from `skills/stitch-design-md/templates/DESIGN.md` into the workspace and tune color palettes and typography to match the product domain.
3. **Verify Compliance**: Run the Google design linter to ensure WCAG AA contrast compliance:
   ```bash
   design.md lint DESIGN.md
   ```
4. **Cloud Synchronization (Recommended)**:
   - Upload the base64-encoded `DESIGN.md` to the project:
     ```json
     {
       "projectId": "<numeric_projectId>",
       "designMdBase64": "<base64_encoded_design_md>"
     }
     ```
   - Bind the design system to the project via `create_design_system_from_design_md`.

---

### Step 4: Scaffold the First Screen (`generate_screen_from_text`)

1. **Enhance Prompt**: Apply the prompt enhancement rules (`stitch-enhance-prompt`):
   - Deconstruct the UI into explicit structural blocks: `TopAppBar`, `HeroBanner`, `StatCardGrid`, `TransactionList`, `BottomNavigation`.
   - Add micro-visual styling: subtle glassmorphism (`backdrop-blur-md`), ambient shadows, and 1px micro-borders.
   - Specify interactive states: active tabs, hover states, scrollable containers.
2. **Generate Screen**: Call `generate_screen_from_text`:
   ```json
   {
     "projectId": "<numeric_projectId>",
     "prompt": "<Enhanced prompt>",
     "deviceType": "MOBILE"
   }
   ```
3. **Present Summary & Next Steps**:
   - Provide the project ID, title, and generated screen preview details.
   - Present clear next actions to the user:
     - **Add Screens**: Generate secondary screens (e.g., settings, details, auth) via `stitch-generate-design`.
     - **Create Variants**: Explore aesthetic alternatives using `generate_variants`.
     - **Iterate**: Refine specific elements using `edit_screens`.
     - **Export Code**: Convert the designs into production React / Vite / Tailwind components via `stitch-react-components`.
