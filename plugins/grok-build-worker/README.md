# Grok build worker

Run one-shot Grok Build jobs from the CLI: submit, poll status, fetch artifacts, and cancel. Local stdio MCP for agents and automation.

**Tools:** `submit_job`, `status`, `fetch_artifacts`, `cancel_job`

**Version:** 1.5.2

## Install

```bash
grok plugin marketplace add OTNworld/grok-plugins
grok plugin install grok-build-worker --trust
```

`--trust` starts a local MCP. Default job mode is `review_readonly`. `build` uses host Grok permissions. `bypassPermissions` is rejected. See [SECURITY.md](../../SECURITY.md).

## MCP start

`.mcp.json` runs `node ${GROK_PLUGIN_ROOT}/mcp/server.js`. Node 18+ only. No npm, no bundle.

Network at runtime: none. No plugin credentials.

## Skills

| Skill | Role |
|-------|------|
| `Grok build worker` | When/how to use the MCP rail |
| `Grok build CLI capabilities` | Profiles, flags, envelope |

## Notes

- Jobs write artifacts under `<workspace>/jobs/<job_id>/` (`GROK_BUILD_JOBS_ROOT` overrides).
- `cwd` must stay under the workspace root (or `GROK_BUILD_CWD_ROOT`).
- Do **not** commit `node_modules` or secrets.
