# Advai Plugin Demo

This repository contains a functional Git-import example for Helix. The plugin is maintained by Advai and connects to Microsoft's public, read-only Microsoft Learn MCP server.

It is intended for end-to-end testing rather than placeholder UI data:

- the repository manifest can be scanned by Helix;
- both bundled skills can be installed and opened;
- the hosted MCP server requires no account or token;
- the MCP endpoint exposes real documentation search, page retrieval, and code-sample tools.

The plugin is not an official Microsoft plugin. Microsoft owns and operates the remote MCP service.

## Repository Layout

```text
.
├── plugins.json
└── plugins/
    └── microsoft-learn-docs/
        ├── assets/
        │   └── icon.png
        ├── plugin.json
        ├── mcp.json
        └── skills/
            ├── microsoft-docs-research/
            │   └── SKILL.md
            └── microsoft-code-samples/
                └── SKILL.md
```

The outer directory is the plugin package ID. Each directory under `skills/` is an individual skill ID.

## Demo Plugin

`microsoft-learn-docs` installs two skills and one hosted MCP server:

- `microsoft-docs-research` searches and fetches Microsoft Learn documentation.
- `microsoft-code-samples` finds official examples for Microsoft SDKs and APIs.
- `microsoft-learn` connects to `https://learn.microsoft.com/api/mcp` using Streamable HTTP without authentication.

The MCP service currently exposes these read-only tools:

- `microsoft_docs_search`
- `microsoft_docs_fetch`
- `microsoft_code_sample_search`

## Test The Import

1. Open **Plugins** in Helix and choose **Import**.
2. Select **Import plugin from a Git repository**.
3. Enter `https://github.com/Advai-X/advai-plugin-demo` and scan.
4. Enable **Microsoft Learn Research**.
5. Open the installed plugin and refresh **Microsoft Learn MCP** if tool discovery has not run yet.
6. In a conversation, ask: `Find the current Microsoft Learn guidance for Azure Container Apps scaling.`

The imported plugin should show two skills, one MCP server, and three discovered MCP tools.

## Import Contract

An importer should:

1. Clone or fetch the Git repository.
2. Read `plugins.json`.
3. Resolve every plugin path under `plugins/`.
4. Read each `plugin.json`.
5. Validate paths stay inside the repository.
6. Allow local `SKILL.md` files and remote HTTPS MCP servers.
7. Reject local `command`, `args`, arbitrary environment injection, and non-HTTPS MCP URLs for user-imported plugins.

See [docs/plugin-format.md](docs/plugin-format.md) for the complete demo format.
