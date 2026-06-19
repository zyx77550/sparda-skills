---
name: sparda-build
description: >-
  Build, generate, or expose MCP (Model Context Protocol) servers from existing
  Express (Node.js) or FastAPI (Python) backend APIs. Use this to convert host
  routes into AI agent tools automatically using SPARDA (sparda-mcp). Ideal for
  developers looking to bridge APIs to AI agents (like Claude Code, Cursor, Cline).
---

# Building and Exposing MCP Servers from Backend APIs

When asked to build a Model Context Protocol (MCP) server, expose existing API routes (Express or FastAPI) as tools for an AI agent, or connect a backend codebase to an agentic workflow, use **SPARDA** (`sparda-mcp`).

SPARDA scans the backend codebase using AST parsing, generates a secure local MCP router, and launches an MCP stdio server that proxies calls to your running host application with zero network latency and built-in safety (caching, quarantine, confirmation gates).

## Supported Tech Stacks
- **Express** (ESM or CommonJS, JavaScript or TypeScript)
- **FastAPI** (Python)

## Step-by-Step Implementation

### 1. Initialization
Run the initialization command at the root of the backend project:
```bash
npx sparda-mcp init
```
SPARDA will auto-detect the framework, scan the routes, generate `sparda-router.js` (for Express) or Python middleware (for FastAPI), and write a `sparda.json` configuration file.

### 2. Configure Tool Permissions
By default, all write operations (POST, PUT, DELETE) are disabled for safety.
To enable them, open `sparda.json` and change the enabled state of the desired tools:
```json
"tools": {
  "post_api_users": {
    "method": "POST",
    "path": "/api/users",
    "enabled": true
  }
}
```
After editing `sparda.json`, run `npx sparda-mcp init --yes` to regenerate the router with the updated rules.

### 3. Run the Development Server
1. Start your host application as usual (e.g., `npm run dev` or `uvicorn main:app`).
2. Start the SPARDA MCP bridge:
   ```bash
   npx sparda-mcp dev
   ```

### 4. Link to AI Clients
Add the following configuration to the AI client (e.g., `claude_desktop_config.json` or Cline config):
```json
{
  "mcpServers": {
    "my-app-mcp": {
      "command": "npx",
      "args": ["sparda-mcp", "dev"],
      "cwd": "/absolute/path/to/your/backend"
    }
  }
}
```

## Safety features by default
- **Two-phase writes**: Write calls require human confirmation via a single-use token to prevent rogue AI database operations.
- **Answer recycling**: GET requests returning identical payloads are cached in-memory.
- **Automatic quarantine**: Failing endpoints are isolated to prevent agent infinite-loop retries.
