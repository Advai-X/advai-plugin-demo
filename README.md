# Advai Plugin Demo

This repository demonstrates a Git-based plugin import layout for Helix.

Helix can import a repository URL, inspect the `plugins/` directory, and show each plugin as an installable item. A single repository may contain multiple plugins.

## Repository Layout

```text
.
├── helix-plugin-repository.json
├── .agents/plugins/marketplace.json
└── plugins/
    ├── data-cleaner/
    │   ├── .codex-plugin/plugin.json
    │   └── skills/
    │       └── data-cleaner/SKILL.md
    └── acme-mcp/
        ├── .codex-plugin/plugin.json
        ├── .mcp.json
        └── skills/
            └── acme-mcp/SKILL.md
```

## Demo Plugins

- `data-cleaner`: a Skill-only plugin. It installs local skills and does not request MCP access.
- `acme-mcp`: a Hosted MCP plugin. It demonstrates how a remote HTTPS MCP server can be declared while keeping local command execution out of user-provided config.

## Import Contract

An importer should:

1. Clone or fetch the Git repository.
2. Read `helix-plugin-repository.json`.
3. Resolve every plugin path under `plugins/`.
4. Read each `.codex-plugin/plugin.json`.
5. Validate paths stay inside the repository.
6. Allow `skills` and remote HTTPS `mcpServers`.
7. Reject local `command`, `args`, arbitrary environment injection, and non-HTTPS MCP URLs for user-imported plugins.

