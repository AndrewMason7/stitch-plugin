# Stitch Plugin for Antigravity

An independent Antigravity plugin for Google Stitch that integrates AI-assisted cloud UI/UX prototyping, 15 verified MCP tools, 17 standardized design-to-code skills, and the `@google/design.md` token engine.

[![Antigravity](https://img.shields.io/badge/Antigravity-Plugin-4285F4?logo=google&logoColor=white)](https://antigravity.google)
[![Google Stitch](https://img.shields.io/badge/Google-Stitch-EA4335?logo=google&logoColor=white)](https://stitch.withgoogle.com)
[![Status](https://img.shields.io/badge/Status-Beta-34A853)](#overview)
[![MCP Tools](https://img.shields.io/badge/MCP%20Tools-15%20Verified-FBBC05)](#mcp-server-tools)
[![Skills](https://img.shields.io/badge/Skills-17%20Standardized-4285F4)](#bundled-skills)
[![License](https://img.shields.io/badge/License-Apache--2.0-blue.svg)](LICENSE)

> [!NOTE]
> **Community Disclaimer:** This project is an independent community adaptation based on open-source Stitch skills originally developed by Google Labs. It is not an officially supported Google product, and is not affiliated with, sponsored by, or endorsed by Google LLC.

---

## Table of contents

- [Overview](#overview)
- [Key features](#key-features)
- [Directory structure](#directory-structure)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Quickstart](#quickstart)
- [Configuration and security](#configuration-and-security)
- [MCP server tools](#mcp-server-tools)
- [Bundled skills](#bundled-skills)
- [Custom agent: stitch-designer](#custom-agent-stitch-designer)
- [Design token workflow](#design-token-workflow)
- [License](#license)
- [Disclaimer](#disclaimer)

---

## Overview

The Stitch Plugin enables AI agents in Google Antigravity to design, prototype, and build production-ready user interfaces using Google Stitch. It bridges high-level natural language intent with cloud-rendered UI mockups and extracts those mockups into modular frontend code (React, Vite, Tailwind CSS, and React Native).

By combining Stitch's remote Model Context Protocol (MCP) server with token specifications from `@google/design.md`, this plugin enables autonomous design loops, semantic token synchronization, and high-fidelity component generation without manual design-to-code translation.

---

## Key features

- **Cloud UI generation**: Create, edit, and generate variants of web and mobile interface mockups through Google Stitch.
- **15 verified MCP tools**: Direct integration with Stitch's hosted endpoint (`stitch.googleapis.com/mcp`) audited against upstream schemas.
- **Prompt enhancement pipeline**: Automatically expands brief UI requests into professional design briefs with typographic hierarchy, micro-interactions, and contrast ratios.
- **Semantic token architecture**: Full support for Google's `@google/design.md` standard with automated WCAG AA contrast verification and token export.
- **Production code conversion**: Export generated screens directly into modular React + Vite components, styled React Native views, or shadcn/ui components.
- **Specialized custom agent**: Includes the `stitch-designer` custom agent and the `/stitch` slash command for conversational design workflows.
- **Bundled documentation and references**: Comprehensive technical guides, tool schemas, prompt recipes, and `DESIGN.md` templates are bundled directly inside respective skill directories (`references/` and `templates/`) for instant agent and developer access.
- **Zero-secret configuration**: Uses runtime environment variable resolution (`${STITCH_API_KEY}`) to prevent credential exposure.

---

## Directory structure

This repository follows the official Antigravity plugin directory layout:

```text
stitch/
├── plugin.json                 # Plugin manifest, branding, and metadata
├── installed_version.json       # Version tracking (v1.0.0)
├── mcp_config.json             # Remote Google Stitch HTTP MCP endpoint config
├── README.md                   # Plugin documentation and user guide
├── assets/
│   └── logo.png                # Plugin logo asset
├── agents/
│   └── stitch-designer.md      # Specialized UI/UX & prototyping custom agent
├── rules/
│   └── AGENTS.md               # Architectural rules, guidelines, and quality standards
└── skills/                     # 17 standardized Stitch engineering skills
    ├── stitch/                 # Master orchestrator & /stitch command handler
    ├── stitch-code-to-design/  # Reverse-engineers frontend code into Stitch
    ├── stitch-design-md/       # DESIGN.md synthesis, spec guides & starter templates
    ├── stitch-enhance-prompt/  # Prompt enhancement pipeline & vocabulary recipes
    ├── stitch-extract-design-md/   # Extracts DESIGN.md from existing codebases
    ├── stitch-extract-static-html/ # Captures self-contained HTML from web applications
    ├── stitch-generate-design/ # Screen generation & MCP tool references
    ├── stitch-loop/            # Autonomous baton-passing site build loop
    ├── stitch-manage-design-system/ # Manages and applies design systems in Stitch
    ├── stitch-react-components/# Converts Stitch HTML into Vite/React components
    ├── stitch-react-native/    # Converts Stitch HTML into React Native components
    ├── stitch-react-vite-dashboard/ # Generates production dashboards with TanStack Query
    ├── stitch-remotion/        # Generates animated walkthrough videos with Remotion
    ├── stitch-shadcn-ui/       # Integrates shadcn/ui component library
    ├── stitch-site-md/         # Synthesizes site constitutions (SITE.md)
    ├── stitch-taste-design/    # Enforces anti-generic design standards
    └── stitch-upload-to-stitch/# Uploads assets and design markdown to Stitch projects
```

---

## Prerequisites

Before using the plugin, verify that your environment meets the following requirements:

1. **Google Antigravity CLI (`agy`)**: Installed and available on your system path.
2. **Node.js**: Version 18.0.0 or later.
3. **`@google/design.md` CLI**: Install globally using npm:
   ```bash
   npm install -g @google/design.md
   ```
4. **Stitch API Key**: An active API key obtained from the [Google Stitch website](https://stitch.withgoogle.com).

---

## Installation

Install the plugin directly from GitHub into Google Antigravity:

### Via Shell / Terminal

```bash
agy plugin install https://github.com/AndrewMason7/stitch-plugin
```

### Via Antigravity CLI / TUI

```text
/plugin install https://github.com/AndrewMason7/stitch-plugin
```

---

## Quickstart

Follow these steps to configure and use the Stitch plugin:

### 1. Configure your API key

Obtain your API key from the [Stitch website](https://stitch.withgoogle.com).

Add your API key to your shell profile (`~/.zshrc` or `~/.bashrc`):

```bash
export STITCH_API_KEY="YOUR_STITCH_API_KEY"
```

Then reload your shell configuration (e.g. `source ~/.zshrc` or `source ~/.bashrc`).

### 2. Generate your first UI screen

In your Antigravity chat session, run the `/stitch` command:

```text
/stitch Design a modern dark-mode fintech mobile app
```

The agent will expand your request, create a project container via the Stitch MCP, generate screen variants, and present the preview.

---

## Configuration and security

### Remote MCP configuration

The plugin connects to Stitch through `mcp_config.json`:

```json
{
  "mcpServers": {
    "stitch": {
      "serverUrl": "https://stitch.googleapis.com/mcp",
      "headers": {
        "X-Goog-Api-Key": "${STITCH_API_KEY}"
      },
      "variables": [
        {
          "name": "STITCH_API_KEY",
          "description": "Google Stitch API Key"
        }
      ]
    }
  }
}
```

### Credential safety

- **Environment variables only**: Never commit raw API keys to repository files or markdown documents. The plugin resolves credentials at runtime via `${STITCH_API_KEY}`.
- **Git protection**: A pre-configured `.gitignore` prevents logs, caches, and scratch files from being tracked.

---

## MCP server tools

The plugin exposes 15 tools through the `stitch` server name (`ServerName: "stitch"`):

| Tool name | Description | Key parameters |
| :--- | :--- | :--- |
| `create_project` | Creates a new Stitch workspace project container. | `title` *(optional)* |
| `list_projects` | Lists all Stitch projects accessible to the authenticated user. | `filter` (`view=owned` or `view=shared`) |
| `get_project` | Retrieves project metadata, screen lists, and design systems. | `name` (`projects/{project_id}`) |
| `delete_project` | Permanently deletes a Stitch project. | `name` (`projects/{project_id}`) |
| `list_screens` | Lists all UI screens associated with a project. | `projectId` |
| `get_screen` | Retrieves screen HTML source, preview images, and metadata. | `name` (`projects/{project_id}/screens/{screen_id}`) |
| `generate_screen_from_text` | Generates a new UI screen mockup from a natural language prompt. | `projectId`, `prompt`, `deviceType`, `designSystem`, `modelId` |
| `edit_screens` | Modifies existing screens using iterative prompts. | `projectId`, `selectedScreenIds`, `prompt`, `deviceType`, `modelId` |
| `generate_variants` | Creates visual design alternatives of existing screens. | `projectId`, `selectedScreenIds`, `prompt`, `variantOptions` |
| `upload_design_md` | Uploads a base64-encoded `DESIGN.md` file to a project. | `projectId`, `designMdBase64` |
| `create_design_system_from_design_md` | Creates a formal Stitch design system from an uploaded `DESIGN.md`. | `projectId`, `selectedScreenInstance`, `deviceType` |
| `list_design_systems` | Lists available design systems globally or for a specific project. | `projectId` *(optional)* |
| `create_design_system` | Creates a custom design system with explicit token definitions. | `designSystem`, `projectId` *(optional)* |
| `update_design_system` | Updates token values for an existing design system asset. | `name` (`assets/{asset_id}`), `projectId`, `designSystem` |
| `apply_design_system` | Applies a design system across designated screen instances. | `assetId`, `projectId`, `selectedScreenInstances` |

For detailed payload schemas and response structures, see the [MCP tools reference guide](skills/stitch-generate-design/references/mcp-tools.md).

---

## Bundled skills

The plugin includes 17 standardized skills, organized by functional area:

### Orchestration and ideation

- **`stitch`**: Handles project creation (`create_project`), design system initialization, initial UI bootstrapping, and the `/stitch` command.
- **`stitch-generate-design`**: Full generation pipeline with prompt expansion and MCP tool calls.
- **`stitch-enhance-prompt`**: Expands brief user inputs into complete design briefs. Consult the [prompt enhancement recipes](skills/stitch-enhance-prompt/references/prompt-enhancement-recipes.md) for domain-specific patterns.
- **`stitch-loop`**: Autonomous baton-passing loop for building complete multi-page web applications.
- **`stitch-site-md`**: Synthesizes a structured project constitution into `SITE.md`.

### Design system and tokens

- **`stitch-design-md`**: Synthesizes design tokens into markdown specifications using the [DESIGN.md starter template](skills/stitch-design-md/templates/DESIGN.md).
- **`stitch-manage-design-system`**: Creates, updates, and applies design systems in the Stitch cloud. Consult the [design system synchronization guide](skills/stitch-design-md/references/design-systems.md).
- **`stitch-taste-design`**: Enforces strict typographic contrast, color calibration, and micro-motion standards.
- **`stitch-upload-to-stitch`**: Encodes and uploads local assets and documentation to Stitch projects.

### Code conversion and export

- **`stitch-code-to-design`**: Reverse-engineers existing frontend code into Stitch cloud mockups.
- **`stitch-extract-design-md`**: Extracts token definitions from existing codebases (React, Vue, Svelte, Angular, CSS).
- **`stitch-extract-static-html`**: Inlines styles and assets to capture self-contained static HTML.
- **`stitch-react-components`**: Converts generated Stitch HTML into modular React + Vite components following the [design-to-code conversion guide](skills/stitch-react-components/references/design-to-code.md).
- **`stitch-react-native`**: Converts Stitch HTML mockups into native React Native StyleSheet components.
- **`stitch-react-vite-dashboard`**: Generates production dashboards integrated with TanStack Query.
- **`stitch-shadcn-ui`**: Integrates shadcn/ui components with extracted Stitch design systems.
- **`stitch-remotion`**: Generates automated video tours and animated walkthroughs of Stitch screens.

---

## Custom agent: stitch-designer

For complex, multi-screen, or end-to-end prototyping tasks, select the specialized **`stitch-designer`** custom agent directly from the agent picker inside the Antigravity application:

1. Open the agent picker dropdown in the chat input area.
2. Choose **`stitch-designer`** (UI/UX Prototyper).
3. Enter your design prompt or product brief (for example: *\"Design a multi-screen healthcare telemetry dashboard with dark mode and export to React components\"*).

The custom agent operates autonomously using the prompt enhancement pipeline and design system rules defined in [agents/stitch-designer.md](agents/stitch-designer.md).

---

## Design token workflow

Manage and export design tokens using the official `@google/design.md` toolsuite:

### 1. Validate token syntax and accessibility

Run the linter to verify formatting, token references, and WCAG AA contrast:

```bash
design.md lint skills/stitch-design-md/templates/DESIGN.md
```

### 2. Export tokens to Tailwind CSS v4

Export directly to modern CSS `@theme` variables:

```bash
design.md export DESIGN.md --format css-tailwind > src/theme.css
```

### 3. Export tokens to Tailwind CSS v3

Export to `tailwind.config.js` theme extension format:

```bash
design.md export DESIGN.md --format json-tailwind > tailwind.tokens.json
```

For the complete 3-step cloud synchronization procedure, see the [cloud design system guide](skills/stitch-design-md/references/design-systems.md).

---

## License

Distributed under the Apache License 2.0. See [LICENSE](LICENSE) and [NOTICE](NOTICE) for details.

---

## Disclaimer

This project is provided \"as is\", without warranties or conditions of any kind, either express or implied. This repository is an independent community project and is not an official product, service, or distribution of Google LLC or Alphabet Inc. Google, Google Stitch, and Google Antigravity are trademarks of Google LLC. Use of these trademarks in this project is strictly nominative and does not imply any affiliation, sponsorship, endorsement, or approval by Google LLC.
