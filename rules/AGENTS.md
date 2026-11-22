# Autodesk Fusion 360 Guidelines

- **Local MCP Server Connection**: The `fusion-360` MCP server connects to a live local Autodesk Fusion desktop session over Streamable HTTP at `http://127.0.0.1:27182/mcp`. If tools are unavailable or connection errors occur, ask the user to confirm Autodesk Fusion is running and **Preferences > General > API > Fusion MCP Server** is enabled on port `27182`.
- **Verify Document Units & Orientation First**: Before creating or modifying geometry, inspect the active document's units (e.g., `mm` vs `in`) and up-axis convention (Z-up vs Y-up) rather than assuming defaults.
- **Prefer Parametric Modeling**: Define named user parameters for key dimensions (length, width, thickness, hole diameters, clearances) and keep sketches constrained so the user can adjust the design later in Fusion's timeline.
- **Confirm Destructive Operations**: Before deleting bodies, sketches, components, or clearing timeline features in an active user design, summarize what will be removed and ask for confirmation unless the user explicitly requested deletion.
- **Use Discovered Tool Schemas**: Autodesk Fusion's MCP server registers tools dynamically at connection time. Always rely on the tool definitions currently exposed by the `fusion-360` MCP server rather than assuming hardcoded tool names or arguments.
