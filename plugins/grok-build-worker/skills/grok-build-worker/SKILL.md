---
name: Grok build worker
description: >-
  Use when implementing code via the Grok build worker plugin (build-worker MCP:
  submit_job, status, fetch_artifacts). Require plugin at start; never local
  clone. Read Grok build CLI capabilities for profiles/flags toggles.
---
# Grok build worker

## When
Any **code implementation** (or read-only review / plan-only job) that should land as a one-shot via Grok build worker plugin (MCP tools `submit_job`, `status`, `fetch_artifacts`). Not for durable roles (those are a long-lived bot or Hermes).

**Before composing the job**, also run the companion skill **Grok build CLI capabilities**: profiles, flags, and enable/disable live under your fleet/rails config → `rails.build_worker.capabilities` (or the defaults documented in that skill).

## Plugin gate
Before the first `submit_job` on an install: confirm the marketplace plugin (or account MCP) is installed and usable. If missing: tell the owner to install **Grok build worker** (tools `submit_job`, `status`, `fetch_artifacts`), show connect card if `needsAuth`. Do not invent a substitute rail.

Config hint: `rails.build_worker.plugin` should be `build-worker` (id) and `display_name: Grok build worker`.

## Rail
1. Read capabilities; pick an **enabled** profile (`build` | `review_readonly` | `plan_only`) and only **enabled** flags.
2. `submit_job` with job envelope + clear objective + success criteria (`mode` = profile id). See the capabilities skill for the envelope.
3. `status` until settled.
4. `fetch_artifacts` when needed; prove against the real artefact (PR, commit, log).

## Hard rules
- Never clone the repo locally for this rail
- Never use Cursor CloudAgent as a substitute when this path applies
- Never implement the diff in chat and call it done
- Never use a disabled capability; offer an enabled alternative instead
- A durable bot or Hermes may orchestrate; the code change still goes through this plugin

## Done means
Job succeeded **and** you re-read the artefact. Say the path: `build-worker` / Grok build worker.

## Failures
Connector error or missing: tell the user plainly; do not silently switch to cookie scrape or local clone without an explicit ask.
