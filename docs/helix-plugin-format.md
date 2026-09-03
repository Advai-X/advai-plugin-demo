# Helix Importable Plugin Format

This document describes the demo format for Helix user-importable plugins.

## Repository Manifest

`helix-plugin-repository.json` lives at the repository root.

```json
{
  "schemaVersion": "1.0",
  "name": "advai-plugin-demo",
  "displayName": "Advai Plugin Demo",
  "description": "Example Git repository containing multiple Helix plugins.",
  "pluginsRoot": "./plugins",
  "manifest": "helix-plugin.json",
  "plugins": [
    {
      "id": "data-cleaner",
      "path": "./plugins/data-cleaner"
    }
  ]
}
```

Rules:

- `pluginsRoot` and every plugin `path` must be relative paths inside the repository.
- `manifest` defaults to `helix-plugin.json`.
- A repository may contain one or many plugins.
- Importers should reject symlink or traversal paths that escape the cloned repository.

## Plugin Manifest

Each plugin has one `helix-plugin.json` at the plugin root.

Required fields:

- `schemaVersion`
- `id`
- `name`
- `version`
- `publisher`
- `description`
- `category`
- `skills`

Optional fields:

- `longDescription`
- `homepage`
- `repository`
- `license`
- `keywords`
- `capabilities`
- `brandColor`
- `starterPrompts`
- `mcpServers`

## Skills

`skills` is an array of local skill descriptors:

```json
{
  "id": "data-cleaner",
  "name": "data-cleaner",
  "description": "Inspect and clean tabular data.",
  "path": "./skills/data-cleaner/SKILL.md"
}
```

Rules:

- Skill paths must point to `SKILL.md` files inside the plugin root.
- Skill IDs must be unique within a repository import.
- Importers may mark skills as needing review when the file mentions shell, network, file writes, or MCP.

## Hosted MCP

`mcpServers` may point to `helix-mcp.json`.

```json
{
  "mcpServers": [
    {
      "id": "acme",
      "name": "Acme MCP",
      "transport": "http",
      "url": "https://mcp.example.com/sse",
      "auth": "oauth",
      "scopes": ["pages.read", "pages.write"]
    }
  ]
}
```

For user-imported plugins, the first public version should only allow hosted MCP:

- `transport` must be `http`.
- `url` must be HTTPS.
- `auth` may be `none`, `secret`, or `oauth`.
- `oauth` should use MCP OAuth discovery from the server URL.
- User-imported manifests must not provide OAuth authorization or token endpoints.

Rejected for user-imported plugins:

- Local `command`
- `args`
- arbitrary `env`
- arbitrary HTTP/API adapter definitions
- CLI adapter definitions
- non-HTTPS URLs
- localhost or private-network MCP URLs by default

