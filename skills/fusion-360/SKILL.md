---
name: fusion-360
description: >-
  Workflows and best practices for interacting with a local Autodesk Fusion 360
  desktop session via the fusion-360 MCP server (http://127.0.0.1:27182/mcp).
  Use when inspecting active Fusion documents, creating or editing parametric
  3D CAD models, managing sketches, features, parameters, or troubleshooting
  the local Fusion MCP connection.
---

# Autodesk Fusion 360 CAD Workflow

This skill guides real-time parametric CAD modeling, inspection, and automation
through the local **Autodesk Fusion MCP Server** (`http://127.0.0.1:27182/mcp`),
configured under the `fusion-360` MCP server in this plugin.

## 1. Prerequisites & Connection Check

The `fusion-360` MCP server uses **Streamable HTTP** to talk to the active
Autodesk Fusion desktop instance on this machine.

If `fusion-360` MCP tools are missing or return connection errors:
1. Verify **Autodesk Fusion** is open and running locally.
2. In Fusion, open **Preferences > General > API** and ensure **Fusion MCP Server (runs locally on this device)** is checked.
3. Confirm the configured port matches `27182` (or update `mcp_config.json` in this plugin if the user configured a custom port).
4. Remember that tools from the Fusion MCP server are discovered dynamically on connection; once Fusion is running, reconnect/refresh the MCP server or start a new turn.

## 2. Inspect Before Modifying

Before creating or editing geometry in an existing document:
1. Inspect the active document structure: root component, sub-components, bodies, sketches, construction geometry, and existing user parameters.
2. Check the **document units** (`mm`, `cm`, `in`, etc.) and **coordinate orientation** (typically Z-up in Fusion, though some users use Y-up).
3. Note that Fusion's internal API uses centimeters (`cm`) for raw length values in some APIs while UI/parameter expressions use document units — always verify the unit expectation of each MCP tool's schema before passing numeric values.

## 3. Clean Parametric CAD Modeling Order

Follow standard Fusion 360 parametric best practices so the resulting timeline
is clean, readable, and easy to edit:

1. **Define User Parameters First**: Create named parameters for key dimensions (e.g., `wall_thickness`, `mount_hole_dia`, `clearance`, `overall_width`) before sketching.
2. **Organize with Components**: For multi-part assemblies, create separate components rather than piling unrelated bodies into the root component.
3. **Name Features Clearly**: Give sketches, bodies, and components descriptive names (e.g., `BaseProfile_Sketch`, `MainBracket`, `M4_ClearanceHoles`).
4. **Build in Logical Feature Order**:
   - Reference planes / axes
   - Base sketches (fully constrained to the origin where possible)
   - Primary solid features (Extrude, Revolve, Sweep, Loft)
   - Secondary cuts, holes, patterns, and ribs
   - Cosmetic / stress-relief features (**Fillets** and **Chamfers**) **last**, so they don't break upstream references.
5. **Respect Manufacturing Clearances**:
   - When designing mating parts, ask whether the part is for 3D printing (FDM/SLA), laser cutting, or CNC machining, and incorporate appropriate clearance parameters (e.g., `0.2 mm`–`0.4 mm` typical FDM fit tolerance, standard fastener clearance holes).

## 4. Verification & Safety

- After creating or modifying features, query the resulting body properties (bounding box, volume, feature/timeline status, or viewport capture if exposed) to confirm the geometry matches intent and has no timeline warnings/errors.
- Avoid destructive changes (deleting user bodies, sketches, or components) without first confirming with the user, unless they explicitly asked to remove them.
- If an operation fails in Fusion's timeline, report the exact failure reason and propose a clean fix (e.g., adjusting sketch constraints, extrusion extent, or fillet radius) rather than stacking workarounds.
