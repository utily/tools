---
name: coding-security
description: "Apply TypeScript and application security coding rules. Use when: security review, input validation, untrusted input handling, redirect safety, callback verification, HTML/query encoding, regex safety, dynamic evaluation risks, boundary hardening, cloudflare worker hardening."
---

# Coding Security

Use this skill to enforce security-focused code authoring and review.

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
