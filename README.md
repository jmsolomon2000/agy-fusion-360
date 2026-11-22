# Autodesk Fusion 360 Plugin for Antigravity

Connects Antigravity to your local **Autodesk Fusion 360** desktop session using Fusion's built-in local MCP server (`http://127.0.0.1:27182/mcp`).

## What's Included

- **MCP Server (`mcp_config.json`)**: Connects to `http://127.0.0.1:27182/mcp` via Streamable HTTP under the `fusion-360` server name.
- **Skill (`skills/fusion-360/SKILL.md`)**: Guides parametric CAD modeling order, unit checks, dynamic tool discovery, and connection troubleshooting.
- **Rules (`rules/AGENTS.md`)**: Keeps CAD edits unit-aware, parametric, and safe from accidental destructive changes while the plugin is enabled.
- **Logo (`assets/logo.svg`)**: Custom vector CAD icon for the plugin UI.

## Prerequisites

1. Launch **Autodesk Fusion** on your computer and keep it running while using this plugin.
2. In Fusion, open **Preferences > General > API**.
3. Enable **Fusion MCP Server (runs locally on this device)**.
4. Leave the default port set to **`27182`** (or update the URL in `mcp_config.json` to match your custom port).

## Installation on Other Machines

### Option A: Using the Antigravity CLI (`agy`)
```bash
agy plugin install https://github.com/jmsolomon2000/agy-fusion-360
```

### Option B: Clone Directly into the Global Plugins Directory
- **Windows (PowerShell):**
  ```powershell
  git clone https://github.com/jmsolomon2000/agy-fusion-360.git "$env:USERPROFILE\.gemini\config\plugins\fusion-360"
  ```
- **macOS / Linux:**
  ```bash
  git clone https://github.com/jmsolomon2000/agy-fusion-360.git ~/.gemini/config/plugins/fusion-360
  ```

Antigravity discovers the plugin automatically — no restart required.

## Troubleshooting

- **Tools not appearing**: Make sure Autodesk Fusion is open with the MCP server enabled, then refresh MCP servers in Antigravity (**Additional Options (...) > MCP Servers**).
- **Custom port**: Edit `mcp_config.json` inside the plugin folder and change `http://127.0.0.1:27182/mcp` to your chosen port.
