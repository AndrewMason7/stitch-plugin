# Google Stitch MCP Tool Reference Guide

The Google Stitch Model Context Protocol (MCP) server exposes **15 dedicated tools** enabling AI agents to programmatically create, manage, and iterate on UI screens, design systems, and frontend code containers.

All tools communicate with the remote Stitch endpoint over HTTP via `ServerName: "stitch"`.

---

## 1. Project Management

### `create_project`
Creates a new Stitch project container for UI designs and frontend code.
- **Parameters:**
  - `title` (string, *optional*): The title of the project (e.g. `"B2B Analytics Platform"`).
- **Return Value:** Project object with resource name `projects/{projectId}`.
- **Example Call:**
  ```python
  call_mcp_tool(
      ServerName="stitch",
      ToolName="create_project",
      Arguments={"title": "Crypto Portfolio Tracker"}
  )
  ```

### `list_projects`
Lists all Stitch projects accessible to the authenticated user.
- **Parameters:**
  - `filter` (string, *optional*): AIP-160 filter query on the `view` field.
    - `view=owned` (default): Lists only projects owned by the user.
    - `view=shared`: Lists only projects shared with the user.
- **Example Call:**
  ```python
  call_mcp_tool(
      ServerName="stitch",
      ToolName="list_projects",
      Arguments={"filter": "view=owned"}
  )
  ```

### `get_project`
Retrieves detailed information about a specific Stitch project, including screen instances and design systems.
- **Parameters:**
  - `name` (string, **required**): Resource name of the project.
    - Format: `projects/{project}` (e.g. `"projects/4044680601076201931"`).
- **Example Call:**
  ```python
  call_mcp_tool(
      ServerName="stitch",
      ToolName="get_project",
      Arguments={"name": "projects/4044680601076201931"}
  )
  ```

### `delete_project`
Permanently deletes a specific Stitch project and all associated screens.
- **Parameters:**
  - `name` (string, **required**): Resource name of the project to delete.
    - Format: `projects/{project}` (e.g. `"projects/4044680601076201931"`).
- **Important Instructions:**
  - This action cannot be undone. Always prompt the user for confirmation with "yes" or "no" before invoking this tool.
- **Example Call:**
  ```python
  call_mcp_tool(
      ServerName="stitch",
      ToolName="delete_project",
      Arguments={"name": "projects/4044680601076201931"}
  )
  ```

---

## 2. Screen Discovery, Generation & Iteration

### `list_screens`
Lists all screens belonging to a specific Stitch project.
- **Parameters:**
  - `projectId` (string, **required**): Project identifier without the `projects/` prefix (e.g. `"4044680601076201931"`).
- **Example Call:**
  ```python
  call_mcp_tool(
      ServerName="stitch",
      ToolName="list_screens",
      Arguments={"projectId": "4044680601076201931"}
  )
  ```

### `get_screen`
Retrieves detailed metadata, HTML source, and screenshot renditions of a specific screen.
- **Parameters:**
  - `name` (string, **required**): Resource name of the screen.
    - Format: `projects/{project}/screens/{screen}` (e.g. `"projects/4044680601076201931/screens/98b50e2ddc9943efb387052637738f61"`).
- **Example Call:**
  ```python
  call_mcp_tool(
      ServerName="stitch",
      ToolName="get_screen",
      Arguments={"name": "projects/4044680601076201931/screens/98b50e2ddc9943efb387052637738f61"}
  )
  ```

### `generate_screen_from_text`
Generates a new UI screen within a project from an enhanced text prompt.
- **Parameters:**
  - `projectId` (string, **required**): Project identifier without `projects/` prefix (e.g. `"4044680601076201931"`).
  - `prompt` (string, **required**): Enhanced UI prompt detailing components, layout, typography, and styling.
  - `deviceType` (string, *optional*): Target viewport type.
    - Options: `MOBILE` (default, 390px), `DESKTOP` (1280px), `TABLET`, `AGNOSTIC`, `DEVICE_TYPE_UNSPECIFIED`.
  - `designSystem` (string, *optional*): Design system resource name to ensure visual consistency (e.g. `"assets/15996705518239280238"`).
  - `modelId` (string, *optional*): Gemini generation model.
    - Options: `GEMINI_3_8_FLASH`, `GEMINI_3_5_FLASH_LITE`, `MODEL_ID_UNSPECIFIED`.
- **Operational Guidelines:**
  - Generation may take 1–3 minutes. **Do not retry on timeout.** Poll with `get_screen` every 30 seconds (up to 10 times).
  - Check `output_components`: If it contains suggestions, present them to the user.
- **Example Call:**
  ```python
  call_mcp_tool(
      ServerName="stitch",
      ToolName="generate_screen_from_text",
      Arguments={
          "projectId": "4044680601076201931",
          "prompt": "Modern SaaS analytics dashboard with dark glassmorphism, KPI cards with sparklines, and an asymmetric Bento grid.",
          "deviceType": "DESKTOP"
      }
  )
  ```

### `edit_screens`
Modifies existing screens using natural language instructions.
- **Parameters:**
  - `projectId` (string, **required**): Project identifier without `projects/` prefix.
  - `selectedScreenIds` (array of strings, **required**): Screen IDs to edit (without `screens/` prefix, e.g. `["98b50e2ddc9943efb387052637738f61"]`).
  - `prompt` (string, **required**): Modification prompt.
  - `deviceType` (string, *optional*): `MOBILE`, `DESKTOP`, `TABLET`, `AGNOSTIC`.
  - `modelId` (string, *optional*): `GEMINI_3_8_FLASH`, `GEMINI_3_5_FLASH_LITE`.
- **Example Call:**
  ```python
  call_mcp_tool(
      ServerName="stitch",
      ToolName="edit_screens",
      Arguments={
          "projectId": "4044680601076201931",
          "selectedScreenIds": ["98b50e2ddc9943efb387052637738f61"],
          "prompt": "Convert the feature list into an asymmetric 2-column Bento grid with frosted glass cards."
      }
  )
  ```

### `generate_variants`
Produces creative or layout variations of existing screens.
- **Parameters:**
  - `projectId` (string, **required**): Project identifier without `projects/` prefix.
  - `selectedScreenIds` (array of strings, **required**): Target screen IDs to generate variants for.
  - `prompt` (string, **required**): Variation guidance prompt.
  - `variantOptions` (object, **required**):
    - `variantCount` (integer, *optional*): Number of variants (1–5, default: 3).
    - `creativeRange` (string, *optional*): `REFINE` (subtle), `EXPLORE` (balanced, default), `REIMAGINE` (radical).
    - `aspects` (array of strings, *optional*): Specific dimensions to vary (`LAYOUT`, `COLOR_SCHEME`, `IMAGES`, `TEXT_FONT`, `TEXT_CONTENT`).
  - `deviceType` (string, *optional*): `MOBILE`, `DESKTOP`, `TABLET`, `AGNOSTIC`.
  - `modelId` (string, *optional*): `GEMINI_3_8_FLASH`, `GEMINI_3_5_FLASH_LITE`.
- **Example Call:**
  ```python
  call_mcp_tool(
      ServerName="stitch",
      ToolName="generate_variants",
      Arguments={
          "projectId": "4044680601076201931",
          "selectedScreenIds": ["98b50e2ddc9943efb387052637738f61"],
          "prompt": "Explore high-variance asymmetric editorial layouts.",
          "variantOptions": {
              "variantCount": 3,
              "creativeRange": "EXPLORE",
              "aspects": ["LAYOUT", "COLOR_SCHEME"]
          }
      }
  )
  ```

---

## 3. Design System & Token Management

### `upload_design_md`
Uploads a base64-encoded UTF-8 `DESIGN.md` file to a Stitch project.
- **Parameters:**
  - `projectId` (string, **required**): Target project ID without `projects/` prefix.
  - `designMdBase64` (string, **required**): Base64-encoded UTF-8 string of `DESIGN.md`.
- **Operational Rule:**
  - Must call `create_design_system_from_design_md` immediately after this tool to extract tokens into a design system.
- **Example Call:**
  ```python
  import base64
  with open("DESIGN.md", "rb") as f:
      b64_content = base64.b64encode(f.read()).decode("utf-8")

  call_mcp_tool(
      ServerName="stitch",
      ToolName="upload_design_md",
      Arguments={
          "projectId": "4044680601076201931",
          "designMdBase64": b64_content
      }
  )
  ```

### `create_design_system_from_design_md`
Creates a design system from a previously uploaded `DESIGN.md` and displays a preview in Stitch.
- **Parameters:**
  - `projectId` (string, **required**): Target project ID without `projects/` prefix.
  - `selectedScreenInstance` (object, **required**): Screen instance returned after uploading `DESIGN.md`:
    - `id` (string, **required**): Screen instance ID (from `get_project`, **not** source screen ID).
    - `sourceScreen` (string, **required**): Resource name (`projects/{project}/screens/{screen}`).
  - `deviceType` (string, *optional*): `MOBILE`, `DESKTOP`, `TABLET`, `AGNOSTIC`.
- **Example Call:**
  ```python
  call_mcp_tool(
      ServerName="stitch",
      ToolName="create_design_system_from_design_md",
      Arguments={
          "projectId": "4044680601076201931",
          "selectedScreenInstance": {
              "id": "inst_12345",
              "sourceScreen": "projects/4044680601076201931/screens/scr_98765"
          },
          "deviceType": "DESKTOP"
      }
  )
  ```

### `create_design_system`
Creates a structured design system with explicit design token parameters.
- **Parameters:**
  - `designSystem` (object, **required**):
    - `colorMode` (string, **required**): `"LIGHT"` or `"DARK"`.
    - `headlineFont` (string, **required**): E.g. `"INTER"`, `"GEIST"`, `"ROBOTO"`, `"SPACE_GROTESK"`, `"OUTFIT"`.
    - `bodyFont` (string, **required**): E.g. `"INTER"`, `"GEIST"`, `"OPEN_SANS"`.
    - `roundness` (string, **required**): `"ROUND_FOUR"`, `"ROUND_EIGHT"`, `"ROUND_TWELVE"`, or `"ROUND_FULL"`.
    - `customColor` (string, **required**): Hex seed color (e.g. `"#047857"`).
    - `overridePrimaryColor`, `overrideSecondaryColor`, `overrideTertiaryColor`, `overrideNeutralColor` (strings, *optional*): Hex overrides.
    - `spacing` (object, *optional*): Map of token name to CSS dimension (e.g. `{"base": "16px"}`).
    - `typography` (object, *optional*): Map of level to `Typography` style object.
    - `designMd` (string, *optional*): Free-form markdown instructions.
  - `projectId` (string, *optional*): Project ID. If omitted, creates a global design system asset.
- **Important Rule:** Must call `update_design_system` immediately after to apply it to the project.

### `update_design_system`
Updates token variables and configuration in an existing design system asset.
- **Parameters:**
  - `name` (string, **required**): Resource name of the design system. Format: `assets/{asset_id}`.
  - `projectId` (string, **required**): Target project ID without `projects/` prefix.
  - `designSystem` (object, **required**): Updated design system parameters (same structure as `create_design_system`).

### `list_design_systems`
Lists design systems associated with a project or global defaults.
- **Parameters:**
  - `projectId` (string, *optional*): Project ID without `projects/` prefix. If omitted, lists all global design systems.
- **Example Call:**
  ```python
  call_mcp_tool(
      ServerName="stitch",
      ToolName="list_design_systems",
      Arguments={"projectId": "4044680601076201931"}
  )
  ```

### `apply_design_system`
Applies a design system asset to selected screen instances across a project.
- **Parameters:**
  - `assetId` (string, **required**): Unique identifier of the design system (without `assets/` prefix, e.g. `"15996705518239280238"`).
  - `projectId` (string, **required**): Project ID without `projects/` prefix.
  - `selectedScreenInstances` (array of objects, **required**):
    - `id` (string, **required**): Screen instance ID (from `get_project`).
    - `sourceScreen` (string, **required**): Resource name (`projects/{project}/screens/{screen}`).
- **Important Rule:** Pass *only* `id` and `sourceScreen` in each instance object; extra position/dimension fields cause invalid argument errors.
- **Example Call:**
  ```python
  call_mcp_tool(
      ServerName="stitch",
      ToolName="apply_design_system",
      Arguments={
          "projectId": "4044680601076201931",
          "assetId": "15996705518239280238",
          "selectedScreenInstances": [
              {
                  "id": "inst_12345",
                  "sourceScreen": "projects/4044680601076201931/screens/scr_98765"
              }
          ]
      }
  )
  ```
