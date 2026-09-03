# Advai Plugin Demo

This repository demonstrates a Git-based plugin import layout for Helix.

Helix can import a repository URL, inspect the `plugins/` directory, and show each plugin as an installable item. A single repository may contain multiple plugins.

## Repository Layout

```text
.
├── plugins.json
└── plugins/
    ├── data-cleaner/
    │   ├── plugin.json
    │   └── skills/
    │       └── data-cleaner/SKILL.md
    └── acme-mcp/
        ├── plugin.json
        ├── mcp.json
        └── skills/
            └── acme-mcp/SKILL.md
```

## Demo Plugins

- `data-cleaner`: a Skill-only plugin. It installs local skills and does not request MCP access.
- `acme-mcp`: a Hosted MCP plugin. It demonstrates how a remote HTTPS MCP server can be declared while keeping local command execution out of user-provided config.

## Import Contract

An importer should:

1. Clone or fetch the Git repository.
2. Read `plugins.json`.
3. Resolve every plugin path under `plugins/`.
4. Read each `plugin.json`.
5. Validate paths stay inside the repository.
6. Allow `skills` and remote HTTPS `mcpServers`.
7. Reject local `command`, `args`, arbitrary environment injection, and non-HTTPS MCP URLs for user-imported plugins.

## Plugin Manifest

Each plugin root contains one `plugin.json` file. This is the public import manifest for a Helix plugin repository.

```json
{
  "schemaVersion": "1.0",
  "id": "data-cleaner",
  "name": "Data Cleaner",
  "version": "0.1.0",
  "publisher": "Advai",
  "description": "Clean and validate table data with Skill-only workflows.",
  "category": "数据与分析",
  "skills": [
    {
      "id": "data-cleaner",
      "path": "./skills/data-cleaner/SKILL.md"
    }
  ]
}
```

Hosted MCP plugins may reference `mcp.json`:

```json
{
  "mcpServers": "./mcp.json"
}
```
