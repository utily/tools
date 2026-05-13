---
name: setup-format
description: "Configure Biome formatting using template-based instructions. Use when: replacing ESLint/Prettier with Biome, adding format scripts, cleaning old lint/format configs, formatting the project."
---

# Setup Format

Use this skill when the user wants a maintainable Biome setup without custom helper scripts.

## Goal

1. Add required dependency and scripts in package.json using _latest Biome version_
2. Ensure biome.json exists and aligns with the template
3. Remove ESLint and Prettier from dependencies and configuration
4. Format the whole project

## Steps

1. Resolve values:
  - Determine the latest available Biome version from npm metadata.
  - Determine the repository default branch from git metadata, and use master if unavailable.

2. Update package.json:
   - Ensure devDependency:
     - @biomejs/biome: <latest-version>
   - Ensure scripts:
     - lint: biome format .
     - format: biome format --write .
   - Remove ESLint/Prettier package entries from:
     - dependencies
     - devDependencies
     - peerDependencies
     - optionalDependencies
   - Remove ESLint/Prettier package.json keys if present:
     - eslintConfig
     - prettier
   - Remove scripts that invoke eslint or prettier.

3. Create biome.json from template:
   - Copy [biome.json.template](./assets/biome.json.template) to project-root biome.json.
   - Replace placeholders:
     - __BIOME_VERSION__ -> latest Biome version
     - __DEFAULT_BRANCH__ -> detected default branch

4. Remove legacy config files from the project root if present:
   - .eslintignore
   - .eslintrc
   - .eslintrc.js
   - .eslintrc.cjs
   - .eslintrc.mjs
   - .eslintrc.json
   - .eslintrc.yaml
   - .eslintrc.yml
   - eslint.config.js
   - eslint.config.cjs
   - eslint.config.mjs
   - eslint.config.ts
   - prettier.config.js
   - prettier.config.cjs
   - prettier.config.mjs
   - prettier.config.ts
   - .prettierignore
   - .prettierrc
   - .prettierrc.js
   - .prettierrc.cjs
   - .prettierrc.mjs
   - .prettierrc.json
   - .prettierrc.yaml
   - .prettierrc.yml

5. Install dependencies and format:
   - npm install
   - npm run format

## Notes

- The baseline template lives in:
  - [biome.json.template](./assets/biome.json.template)
- Keep project-specific overrides minimal and documented.