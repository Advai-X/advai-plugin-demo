---
name: draft-pages
description: Use when the user wants to create, update, or prepare draft Acme workspace pages through the hosted Acme MCP server.
---

# Draft Pages

Use this skill for write-oriented Acme workspace page workflows.

## Workflow

1. Confirm the target workspace, parent page, and intended audience.
2. Discover available MCP tools before calling any tool.
3. Draft the page content in chat before creating or updating a remote page.
4. Ask for confirmation before create, update, publish, delete, or sharing operations.
5. Report the MCP tool used and the resulting page identifier.

## MCP

- Server ID: `acme`
- Transport: hosted HTTPS MCP
- Authentication: OAuth

## Safety

- Do not ask the user to paste OAuth tokens.
- Do not call tools that were not returned by MCP discovery.
- Treat create, update, delete, publish, and sharing operations as write actions.
