---
name: clean-table
description: Use when the user wants to clean, normalize, or deduplicate tabular data before import or analysis.
---

# Clean Table

Use this skill for CSV, spreadsheet, or table cleanup workflows.

## Workflow

1. Identify the table source and intended downstream use.
2. Profile columns for missing values, inconsistent formats, duplicate keys, and invalid categorical values.
3. Propose cleanup rules before changing data.
4. Preserve the original input and write cleaned output to a separate file.
5. Summarize every transformation that was applied.

## Safety

- Do not overwrite the source file unless the user explicitly asks.
- Ask before deleting rows.
- Treat schema changes, value normalization, and deduplication as user-visible changes.
