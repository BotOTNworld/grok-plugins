# OTNworld Grok plugins

Grok CLI plugin marketplace for the OTNworld org.

## Add the marketplace

```bash
grok plugin marketplace add OTNworld/grok-plugins
```

Private repos use your normal GitHub credentials (`gh auth` / git credential helper).

## Install a plugin

```bash
grok plugin install grok-build-worker --trust
```

`--trust` is required for the plugin’s MCP server and skills to activate.

Refresh / list:

```bash
grok plugin marketplace list
grok plugin marketplace update
grok plugin list
grok plugin details grok-build-worker
```

## Plugins

| Name | Version | Description |
|------|---------|-------------|
| `grok-build-worker` | 1.1.0 | Local stdio MCP for async one-shot build/review/plan jobs |

See [`plugins/grok-build-worker/README.md`](plugins/grok-build-worker/README.md) for MCP `npm install` and skill notes.

## Layout

```text
.grok-plugin/marketplace.json
plugins/grok-build-worker/
  plugin.json
  .mcp.json
  README.md
  mcp/          # stdio server source (run npm install here)
  skills/
```

## Cursor marketplace

Packaging the same plugin for the **Cursor** marketplace is a separate later path. This repository is the Grok CLI marketplace source (`grok plugin marketplace add`).

## Validate locally

```bash
grok plugin validate ./plugins/grok-build-worker
```

## Readable MCP mirror

A public staging mirror with unminified `mcp/server.js` and full `package-lock.json` is at
[`BotOTNworld/grok-plugins`](https://github.com/BotOTNworld/grok-plugins). Prefer installing from this org marketplace (`OTNworld/grok-plugins`).
