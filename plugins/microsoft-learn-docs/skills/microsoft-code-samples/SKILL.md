---
name: microsoft-code-samples
description: Use when the user asks for official code examples involving Azure, .NET, Microsoft 365, Windows, Power Platform, or Microsoft SDKs and APIs.
---

# Microsoft Code Samples

Use the Microsoft Learn MCP server declared by this plugin to find current official examples.

## Workflow

1. Call `microsoft_code_sample_search` with the SDK, class, API, or implementation task.
2. Provide the `language` filter when the user names a programming language.
3. Compare the returned examples and select the one that best matches the user's runtime and SDK version.
4. Use `microsoft_docs_search` and `microsoft_docs_fetch` when surrounding setup or API constraints are required.
5. Adapt examples only after distinguishing Microsoft-provided code from project-specific changes.

## MCP

- Server ID: `microsoft-learn`
- Transport: hosted Streamable HTTP
- Authentication: none
- Expected tools: `microsoft_code_sample_search`, `microsoft_docs_search`, `microsoft_docs_fetch`

## Safety

- Do not claim that adapted code is copied verbatim from Microsoft Learn.
- Preserve source links returned by the MCP tools.
- Do not execute deployment or account-management commands unless the user separately requests them.
