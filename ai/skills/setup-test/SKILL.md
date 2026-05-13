---
name: setup-test
description: "Configure Vitest test setup for a TypeScript project, including migration from Jest and cleanup of Jest artifacts."
---

# Setup Test

Use this skill when the user wants a maintainable Vitest setup and wants to remove Jest usage.

## Goal

1. Add Vitest-based test tooling and scripts
2. Configure test execution through Vite
3. Align TypeScript types for Vitest globals
4. Remove Jest dependencies and Jest configuration
5. Run tests and coverage to verify setup

## Steps

1. Resolve values:
  - Determine the latest available versions from npm metadata for vitest, vite, and @vitest/coverage-v8.
  - Determine the repository default branch from git metadata, and use master if unavailable.

2. Update package.json:
  - Ensure scripts:
    - test: vitest --run
    - coverage: vitest --coverage
  - Remove scripts that invoke jest.
  - Ensure devDependencies:
    - vitest: latest compatible version
    - vite: latest compatible version
    - @vitest/coverage-v8: latest compatible version
  - Remove Jest-related packages from dependencies, devDependencies, peerDependencies, and optionalDependencies:
    - jest
    - @types/jest
    - ts-jest
    - babel-jest
    - jest-environment-jsdom
    - jest-environment-node
    - jest-extended
    - any package whose name starts with @jest/

3. Create vite.config.ts from template:
  - Copy [vite.config.ts.template](./assets/vite.config.ts.template) to project-root vite.config.ts.
  - Ensure test configuration includes:
    - typecheck with tsconfig path set to project tsconfig
    - coverage enabled with reporters text, json, and html
    - cleanOnRerun enabled
    - thresholds for statements, branches, functions, and lines
    - globals enabled
    - include pattern matching spec files in TypeScript and JavaScript
    - testTimeout set to 20000
    - isolate disabled
    - exclude includes node_modules and dist
  - Keep project-specific dependency inlining minimal and documented only when required.

4. Align TypeScript for Vitest:
  - In tsconfig.json compilerOptions types, ensure vitest/globals and node are included.
  - Ensure include and exclude patterns keep coverage, dist, and node_modules out of test type-checking scope.

5. Remove Jest config files from project root if present:
  - jest.config.js
  - jest.config.cjs
  - jest.config.mjs
  - jest.config.ts
  - jest.config.json
  - jest.setup.js
  - jest.setup.ts

6. Remove package.json Jest configuration keys if present:
  - jest

7. Install dependencies and verify:
  - Run npm install.
  - Run npm run test.
  - Run npm run coverage.

## Notes

- The baseline template lives in:
  - [vite.config.ts.template](./assets/vite.config.ts.template)
- Keep the setup self-contained in package.json, vite.config.ts, and tsconfig.json.
- Keep overrides minimal and documented.
- If a repository has unusual runtime dependency loading in tests, document each explicit inline dependency reason in the same file where it is configured.
