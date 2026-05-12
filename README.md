# tools

A centralized, tool-agnostic developer intelligence and automation hub.

## Overview

This repository consolidates AI behavior definitions, automation scripts, team processes, and stable reference knowledge into one place. It is intentionally model- and tool-agnostic so that its contents remain useful regardless of which LLMs, CI systems, or editors are in use.

## Folder Structure

| Folder | Purpose |
|---|---|
| `ai/` | Definitions that shape LLM behavior: agents, prompts, instructions, and skills |
| `automation/` | Executable scripts, CLIs, and CI pipeline configuration |
| `process/` | Human and system workflows for onboarding, releases, and code review |
| `knowledge/` | Stable reference material: architecture decisions, patterns, and conventions |

## Rules

- **`ai/`** affects LLM behavior and must remain model/tool agnostic. Do not include provider-specific syntax or SDK calls.
- **`automation/`** contains executable scripts and CLIs. Every entry point must be runnable without manual setup steps beyond what is documented.
- **`process/`** contains human/system workflows. Keep steps concrete and actionable.
- **`knowledge/`** contains stable reference material. Avoid content that changes frequently; prefer linking to authoritative sources instead.

## Usage

### Clone the repository

```bash
git clone https://github.com/utily/tools.git
cd tools
```

### Run scripts in `automation/`

Browse `automation/scripts/` or `automation/cli/` for available scripts. Each subfolder contains a `README.md` describing what is available and how to invoke it.

```bash
# Example – run a script directly
bash automation/scripts/<script-name>.sh
```

### Extend `ai/` with new agents or prompts

1. Choose the appropriate subfolder (`agents/`, `prompts/`, `instructions/`, or `skills/`).
2. Add a new file following the naming convention used in existing files.
3. Document the new entry in the subfolder's `README.md`.
4. Open a pull request (see Contribution Model below).

## Contribution Model

- All changes are submitted via **pull request**; direct commits to the default branch are not permitted.
- Keep the separation between top-level folders **strict**. An `ai/` file must not contain runnable shell code; an `automation/` file must not contain raw prompt text.
- Prefer small, focused pull requests that touch one folder at a time.
- Update the relevant subfolder `README.md` when adding or removing files.
