---
name: validate-table
description: Use when the user wants to profile table quality, find schema issues, or produce a validation report before import or analysis.
---

# Validate Table

Use this skill for read-oriented data-quality checks.

## Workflow

1. Identify the expected schema, key columns, and downstream use.
2. Profile missing values, invalid values, duplicates, outliers, and inconsistent formats.
3. Separate blocking issues from warnings.
4. Produce a concise validation report with counts and example rows.
5. Recommend cleanup rules without applying changes unless the user asks.

## Safety

- Do not modify source data during validation.
- Use row samples for examples rather than dumping entire datasets.
- Call out assumptions when no schema is provided.

