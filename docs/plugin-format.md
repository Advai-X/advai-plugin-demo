# Importable Plugin Format

This document describes the demo format for user-importable plugin repositories in Helix.

## Repository Manifest

`plugins.json` lives at the repository root.

```json
{
  "schemaVersion": "1.0",
  "name": "advai-plugin-demo",
  "displayName": "Advai Plugin Demo",
  "description": "Importable Helix plugin backed by the public Microsoft Learn MCP server.",
  "pluginsRoot": "./plugins",
  "manifest": "plugin.json",
  "plugins": [
    {
      "id": "microsoft-learn-docs",
      "path": "./plugins/microsoft-learn-docs"
    }
  ]
}
```

Rules:

- `pluginsRoot` and every plugin `path` must be relative paths inside the repository.
- `manifest` defaults to `plugin.json`.
- A repository may contain one or many plugins.
- Importers should reject symlink or traversal paths that escape the cloned repository.

## Plugin Manifest

Each plugin has one `plugin.json` at the plugin root.

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
  "id": "microsoft-docs-research",
  "name": "microsoft-docs-research",
  "description": "Research Microsoft technologies using current Microsoft Learn documentation.",
  "path": "./skills/microsoft-docs-research/SKILL.md"
}
```

Rules:

- Skill paths must point to `SKILL.md` files inside the plugin root.
- Skill IDs must be unique within a repository import.
- Plugin IDs and skill IDs are separate namespaces.
- Importers may mark skills as needing review when the file mentions shell, network, file writes, or MCP.

## Hosted MCP

`mcpServers` may point to `mcp.json`. This repository uses a live, public endpoint:

```json
{
  "mcpServers": [
    {
      "id": "microsoft-learn",
      "name": "Microsoft Learn MCP",
      "description": "Read-only access to official Microsoft Learn documentation and code samples.",
      "transport": "http",
      "url": "https://learn.microsoft.com/api/mcp",
      "auth": "none"
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

- local `command`
- `args`
- arbitrary `env`
- arbitrary HTTP/API adapter definitions
- CLI adapter definitions
- non-HTTPS URLs
- localhost or private-network MCP URLs by default

## Runtime Verification

The Microsoft Learn MCP endpoint has been verified with MCP protocol version `2025-06-18`. A successful `tools/list` response currently includes `microsoft_docs_search`, `microsoft_docs_fetch`, and `microsoft_code_sample_search`.

Remote services can change independently of this repository. Helix should perform tool discovery when the MCP server is enabled and report connection failures separately from manifest validation.
