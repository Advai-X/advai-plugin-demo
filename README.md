# Advai Plugin Demo

This repository demonstrates a Git-based plugin import layout for Helix.

Helix can import a repository URL, inspect the `plugins/` directory, and show each plugin as an installable item. A single repository may contain multiple plugins.

## Repository Layout

```text
.
├── plugins.json
└── plugins/
    ├── data-toolkit/
    │   ├── plugin.json
    │   └── skills/
    │       ├── clean-table/
    │       │   └── SKILL.md
    │       └── validate-table/
    │           └── SKILL.md
    └── acme-workspace/
        ├── plugin.json
        ├── mcp.json
        └── skills/
            ├── search-pages/
            │   └── SKILL.md
            └── draft-pages/
                └── SKILL.md
```

## Demo Plugins

- `data-toolkit`: a Skill-only plugin package. It installs the `clean-table` and `validate-table` skills and does not request MCP access.
- `acme-workspace`: a Hosted MCP plugin package. It installs the `search-pages` and `draft-pages` skills, and demonstrates how a remote HTTPS MCP server can be declared while keeping local command execution out of user-provided config.

The outer directory is the plugin package ID. Directories under `skills/` are individual skill IDs. They are intentionally different in this demo to avoid implying that plugin IDs and skill IDs must match.

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
  "id": "data-toolkit",
  "name": "Data Toolkit",
  "version": "0.1.0",
  "publisher": "Advai",
  "description": "A Skill-only plugin package for cleaning and validating table data.",
  "category": "数据与分析",
  "skills": [
    {
      "id": "clean-table",
      "path": "./skills/clean-table/SKILL.md"
    },
    {
      "id": "validate-table",
      "path": "./skills/validate-table/SKILL.md"
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
