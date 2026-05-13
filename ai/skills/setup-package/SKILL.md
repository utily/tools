---
name: setup-package
description: "Configure npm package metadata and TypeScript build setup for a library package, with optional Node subpath exports."
---

# Setup Package (single canonical template)

Use this skill to configure a maintainable npm + TypeScript library package using a single canonical template that includes Node support by default.

## Goals

- Standardize `package.json` metadata and useful scripts for publishing and building.
- Provide a strict TypeScript development config and a dedicated `tsconfig.build.json` for outputs and declarations.
- Ship one canonical template that includes Node typings and a `./node` export; provide clear instructions for removing those parts for browser-only projects.

## Steps (high level)

1. Resolve basic values
  - Determine required dev dependency versions (e.g., `typescript`, `rimraf`, `@types/node`).
  - Detect repository default branch (use `master` if not available).

2. Apply the single canonical template
  - Use `assets/package.json.template`, `assets/tsconfig.json.template`, and `assets/tsconfig.build.json.template` as the single source of truth.
  - The `package.json.template` includes `@types/node` in `devDependencies` and a `./node` export mapping by default.

3. Node opt-out (when to remove Node items)
  - Remove Node items when your codebase is strictly browser-only and does not import Node built-ins (`fs`, `path`, `crypto`, etc.), does not use Node globals (`process`, `Buffer`), and does not rely on Node-specific runtimes.

4. How to remove Node items (step-by-step)
 - `package.json`: remove the `./node` entry in `exports` and remove `@types/node` from `devDependencies`. Ensure the default `.` export remains pointing to your browser build (e.g. `./dist/index.js`).
 - `tsconfig.json` and other tsconfig files:
   - Remove any `types` directive that lists `node` (for example, remove or edit `"types": ["node"]`). If the `types` array contains multiple entries, remove only `node`.
   - Remove any triple-slash references that request Node types, e.g. `/// <reference types="node" />`.
   - Check for `typeRoots` entries that point to Node-only `@types` folders and adjust them if they prevent other global types from being resolved.
   - Apply these changes consistently across all project tsconfig files (root `tsconfig.json`, `tsconfig.build.json`, and any package or workspace-level TS configs).
   - Quick search commands to find occurrences:

```bash
# find tsconfig files that mention node types
grep -RIn --include="tsconfig*.json" '"types"\s*:\s*\[.*node' . || true
grep -RIn --include="*.ts" "reference types=\"node\"" . || true

# or a broader JSON search for the token "node" inside tsconfig files
jq -e 'has("compilerOptions") and (.compilerOptions.types // [] | index("node") != null)' tsconfig.json >/dev/null 2>&1 || true
```

 - Build outputs: ensure your build pipeline emits a browser-compatible `./dist/index.js` and no steps depend on `index.node.js`.
 - Reinstall and verify: run `npm install` and `npm run build` to confirm nothing uses Node typings or APIs. If TypeScript errors appear after removing Node types, inspect the errors to find residual Node API usage and either guard the code or restore Node typings where required.

5. How to re-enable Node support
  - Re-add `@types/node` to `devDependencies`, add back the `./node` `exports` mapping, and add `node` to `tsconfig.json` `types` if needed. Run `npm install` and `npm run build`.

6. Finalize and verify
  - Run `npm install` and `npm run verify`. Extend `verify` to include tests and lint when `setup-test` and `setup-format` are applied.
