---
name: acme-mcp
description: Use when the user asks to search, create, update, or review Acme workspace pages through the hosted Acme MCP server.
---

# Acme MCP

Use this skill for Acme workspace operations that should go through the hosted MCP server declared by this plugin.

## Workflow

1. Confirm the target Acme workspace or page if it is ambiguous.
2. Discover available MCP tools before calling any tool.
3. Prefer read-only tools for lookup and inspection.
4. For write or destructive tools, summarize the intended change and ask for confirmation before proceeding.
5. Report the MCP tool used and the resulting page or object identifier.

## MCP

- Server ID: `acme`
- Transport: hosted HTTPS MCP
- Authentication: OAuth

## Safety

- Do not ask the user to paste OAuth tokens.
- Do not call tools that were not returned by MCP discovery.
- Treat create, update, delete, publish, and sharing operations as write actions.

