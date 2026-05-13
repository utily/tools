---
name: setup-actions
description: "Clean up existing CI configurations (CircleCI, GitHub Actions, etc.) and replace with a standardized GitHub Actions setup using versioned-branch conventions. Use when: adding CI, replacing CI, migrating from CircleCI, setting up GitHub Actions, automating publish or release workflows."
---

# Setup Actions

Use this skill when the user wants a standardized GitHub Actions CI/CD setup that automatically derives branch names from the package's semver major version.

## Goal

1. Remove any existing CI configuration files from all providers
2. Create a GitHub Actions workflow set covering CI checks, version bumping, and npm publishing
3. Derive branch names from the current major version in package.json — never hardcode them

## Branch Convention

The branch naming convention is derived from the current major version `N` in `package.json`:

| Branch | Purpose |
|---|---|
| `master` | Active development for the current major version — triggers **beta** prereleases |
| `master-{N+1}` | Experimental next major — triggers **alpha** prereleases |
| `master-1` … `master-{N-1}` | Maintenance branches for old majors — trigger **stable** minor/patch bumps |

Examples with `version: "3.1.0"` (N=3):
- `master` → beta prereleases
- `master-4` → alpha prereleases
- `master-1`, `master-2` → stable maintenance bumps

## Steps

### 1. Resolve values

- Read `version` from `package.json` and extract the major version `N`.
- Detect the Node.js version:
  - Read `.nvmrc` if present (strip `v` prefix if any).
  - Otherwise read `engines.node` from `package.json` (strip range operators).
  - Otherwise default to `22`.
- Compute:
  - `__NODE_VERSION__` → detected Node.js version integer (e.g. `22`)
  - `__ALPHA_BRANCH__` → `master-{N+1}` (e.g. `master-4`)
  - `__MAINTENANCE_BRANCHES__` → one YAML list item per line for `master-1` through `master-{N-1}`, indented with 6 spaces (e.g. `      - "master-1"\n      - "master-2"`). Empty string if N ≤ 1.

### 2. Remove legacy CI configuration

Delete these legacy CI configs from the project root when present:

- `.circleci/` (entire directory)
- `.travis.yml`
- `.gitlab-ci.yml`
- `bitbucket-pipelines.yml`
- `azure-pipelines.yml`
- `Jenkinsfile`
- `.drone.yml`

For GitHub Actions, clear existing workflow files in `.github/workflows/` by removing all `.yml` and `.yaml` files, while keeping the directory.

### 3. Create workflow files from templates

Create `.github/workflows/` if it does not exist.
Copy each template from `./assets/` to `.github/workflows/`, replacing placeholders as described in Step 1.
  - Always create:
    - [ci.yml.template](./assets/ci.yml.template) → `.github/workflows/ci.yml`
    - [publish.yml.template](./assets/publish.yml.template) → `.github/workflows/publish.yml`

Notes on version bumps and publish:
- The `publish.yml` template now performs the version bump, tagging, and push as part of the publish job. There is no separate `bump.yml` workflow.
- `publish.yml` determines the release type from the pushed branch (alpha, beta, or latest) and runs the appropriate `npm version` command, then pushes tags.
- Do not create separate `bump-*` workflows; keep bumping inside `publish.yml` to simplify coordination and ensure atomic bump+publish operations.

### 4. Verify

- Confirm `.github/workflows/` contains only the expected workflow files and no legacy files.
- In `.github/workflows/ci.yml`:
  - remove `lint` job if `package.json` has no `lint` script
  - remove `build` job if `package.json` has no `build` script
- If `N <= 1`, remove `"Bump Minor"` from `publish.yml` workflow triggers because `bump-minor.yml` is not created.

## Notes

- Never hardcode branch names — always derive them from the major version in `package.json`.
- The `master` branch always maps to beta. This is a fixed convention regardless of the project name or the default branch name.
- Action versions (`actions/checkout@v4`, `actions/setup-node@v4`, etc.) are pinned in templates — do not change them unless the user requests an upgrade.
- Publish uses npm trusted publishing (OIDC) via `id-token: write`; no `NPM_TOKEN` secret is required in this setup.
- Templates live in:
  - [ci.yml.template](./assets/ci.yml.template)
  - [publish.yml.template](./assets/publish.yml.template)
