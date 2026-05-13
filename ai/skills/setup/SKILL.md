---
name: setup
description: "Run full project setup by explicitly combining all user-level setup skills. Use when: bootstrapping or standardizing a TypeScript/npm package with package metadata, formatting, tests, and CI workflows."
---

# Setup

Use this skill when the user wants complete project setup using all setup-* skills at the user level.

## Included Skills (explicit)

1. [setup-package](../setup-package/SKILL.md)
2. [setup-format](../setup-format/SKILL.md)
3. [setup-test](../setup-test/SKILL.md)
4. [setup-actions](../setup-actions/SKILL.md)
5. [setup-vscode](../setup-vscode/SKILL.md)

## Execution Order

1. Apply `setup-package` to standardize package metadata and TypeScript build setup.
2. Apply `setup-format` to configure Biome and remove ESLint/Prettier artifacts.
3. Apply `setup-test` to configure Vitest and remove Jest artifacts.
4. Apply `setup-actions` to standardize GitHub Actions workflows.
5. Apply `setup-vscode` to configure VS Code settings, extensions, tasks, launch config, and .editorconfig.

## Rules

- Enumerate and follow all skills explicitly; do not skip any.
- Give templates strict priority over existing configurations.
- Compare outcome with templates and point out deviations.
