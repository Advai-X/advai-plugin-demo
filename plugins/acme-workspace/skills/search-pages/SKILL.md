---
name: search-pages
description: Use when the user asks to search, inspect, compare, or summarize Acme workspace pages through the hosted Acme MCP server.
---

# Search Pages

Use this skill for read-oriented Acme workspace operations that should go through the hosted MCP server declared by this plugin.

## Workflow

1. Confirm the target Acme workspace or page if it is ambiguous.
2. Discover available MCP tools before calling any tool.
3. Prefer read-only tools for lookup and inspection.
4. Avoid making changes from this skill.
5. Report the MCP tool used and the resulting page or object identifier.

## MCP

- Server ID: `acme`
- Transport: hosted HTTPS MCP
- Authentication: OAuth

## Safety

- Do not ask the user to paste OAuth tokens.
- Do not call tools that were not returned by MCP discovery.
- If the user asks to create or update a page, switch to the `draft-pages` skill.
