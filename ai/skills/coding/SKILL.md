---
name: coding
description: "Apply both TypeScript maintainability and security coding rules together. Use when: code review, writing new code, refactoring, naming conventions, function shaping, module and export design, input validation, untrusted input handling, redirect safety, HTML/query encoding, regex safety, boundary hardening, code consistency."
---

# Coding

Use this skill to enforce both maintainability and security rules simultaneously.

## Step 1 — Load Maintainability Rules

Follow all steps in [coding-maintainability](../coding-maintainability/SKILL.md).

## Step 1.5 — Load Test Rules

When working on tests or reviewing test code, follow the guidance in [coding-tests](../coding-tests/SKILL.md).

## Step 2 — Load Security Rules

Follow all steps in [coding-security](../coding-security/SKILL.md).

## Resolution Policy

Apply strictest-wins across both skills: if any rules conflict, use the most restrictive interpretation from either skill.
