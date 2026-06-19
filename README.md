# SPARDA MCP Skills

Official Claude Code / AI-agent skills for **SPARDA** (`sparda-mcp`) — turn any
Express or FastAPI app into an MCP server in one command, then drive the
generated server to its full potential.

## Install as a Claude Code plugin

```
/plugin marketplace add zyx77550/sparda-skills
/plugin install sparda@residual-labs
```

That bundles both skills below, so Claude can **build** a SPARDA server from your
app and **drive** it once it's running. The CLI itself ships on npm:

```
npx sparda-mcp init
```

## Skills

- [SKILL.md](./SKILL.md) — drive and interact with a SPARDA-generated MCP server.
- [SKILL-BUILD.md](./SKILL-BUILD.md) — install and build MCP servers from Express and FastAPI backends.

The plugin auto-discovers these from `skills/sparda/` and `skills/sparda-build/`
(copies of the files above); the root copies stay the canonical source for the
[Skills Directory](https://skillsdirectory.com/skills/zyx77550-sparda) listing.
