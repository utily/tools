---
name: coding-maintainability
description: "Apply TypeScript maintainability coding rules. Use when: readability cleanup, refactoring, naming conventions, function shaping, module and export design, API structure, code consistency, long-term maintainability."
---

# Coding Maintainability

Use this skill to enforce maintainability-focused code authoring and review.

## Loading Profiles

- Libraries: load [General Rules](./rules/general/index.md)
- Frontend apps and component libraries: load [General Rules](./rules/general/index.md) and [Frontend Rules](./rules/frontend/index.md)
- Cloudflare workers: load [General Rules](./rules/general/index.md) and [Backend Rules](./rules/backend/index.md)

## Decision Router

1. Start with [General Rules](./rules/general/index.md)
2. Add frontend-specific rules from [Frontend Rules](./rules/frontend/index.md) when working in frontend repositories
3. Add backend-specific rules from [Backend Rules](./rules/backend/index.md) when working in backend repositories

## Resolution Policy

Apply strictest-wins: if multiple rules conflict, use the most restrictive interpretation.
