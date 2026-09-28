---
name: Grok build worker
description: Use when an agent should submit, track, fetch artifacts from, or cancel a one-shot build, review, or plan job on the grok-build-worker MCP.
---
# Grok build worker

## When
One-shot build, review, or plan jobs through this plugin. Not a durable bot.

## Rail
1. Pick `mode`: `review_readonly` (default) | `plan_only` | `build`.
2. `submit_job` with a clear goal and `cwd`.
3. `status` until settled.
4. `fetch_artifacts` and re-read the artefact.

## Rules
- Default mode is read-only.
- `build` uses host Grok permissions. This plugin rejects `bypassPermissions`.
- Do not invent a substitute rail if the MCP is missing; tell the owner to install `grok-build-worker`.
---
