# Grok build worker

Local stdio MCP plugin that runs one-shot Grok Build jobs on the host VM.

**Tools:** `submit_job`, `status`, `fetch_artifacts`, `cancel_job`

**Version:** 1.1.0

## Install (from the OTNworld marketplace)

```bash
grok plugin marketplace add OTNworld/grok-plugins
grok plugin install grok-build-worker --trust
```

Then enable the plugin if your config keeps plugins off by default (`[plugins].enabled` or the Plugins UI).

## First-time MCP deps

The MCP server ships source under `mcp/` without `node_modules`. After install (or after updating the plugin):

```bash
# Plugin root is shown by `grok plugin details grok-build-worker`
cd "$(dirname "$(find ~/.grok -path '*grok-build-worker/mcp/package.json' 2>/dev/null | head -1)")"
npm install
# If package-lock.json is present: npm ci
```

Requires Node.js 18+ on PATH. The `.mcp.json` runs:

```text
node ${CLAUDE_PLUGIN_ROOT}/mcp/server.js
```

(`${CLAUDE_PLUGIN_ROOT}` / `${GROK_PLUGIN_ROOT}` is substituted by the plugin loader.)

## Skills

| Skill | Role |
|-------|------|
| `Grok build worker` | When/how to use the MCP rail |
| `Grok build CLI capabilities` | Profiles, flags, envelope; `tool_admin_cli` default **off** |

## Notes

- Jobs write artifacts under `/workspace/jobs/<job_id>/` by default.
- Do **not** commit `node_modules`, secrets, or a fleet file with host IPs into this plugin.
- `mcp/server.js` on this marketplace may be esbuild-minified for publish size. Readable `server.js` + full `package-lock.json` are on the public mirror: https://github.com/BotOTNworld/grok-plugins (same plugin path).
- Cursor marketplace packaging is a separate, later path — this repo is for the **Grok CLI** marketplace.
