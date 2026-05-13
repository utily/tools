# ai/skills

This folder contains skill definitions that extend an agent's capabilities with discrete, well-scoped behaviors such as querying an API, parsing a file format, or running a linter. Each skill is described in a model-agnostic schema so it can be registered with any tool-calling or function-calling mechanism supported by the host framework.

## Configuring Skills in VS Code

Use VS Code user settings and point Copilot to this folder directly.

No copying into repositories is required.

### 1) Add this folder to Agent Skill paths

Open User Settings JSON and add `chat.agentSkillsLocations`.

```json
{
  "chat.agentSkillsLocations": {
    "/versioned/utily/tools/ai/skills": true
  }
}
```

You can open User Settings JSON with Command Palette: `Preferences: Open User Settings (JSON)`.

### 2) Use this library exclusively (optional)

If you want only this library and not default workspace/user skill folders, disable the built-in locations in the same setting:

```json
{
  "chat.agentSkillsLocations": {
    "~/versioned/utily/tools/ai/skills": true,
    ".github/skills": false,
    ".claude/skills": false,
    ".agents/skills": false,
    "~/.copilot/skills": false,
    "~/.claude/skills": false,
    "~/.agents/skills": false
  }
}
```

### 3) Use skill-by-skill in chat

After adding the path, skills in this folder are available as slash commands.

Examples:

```text
/coding review this module for maintainability and security
/coding-tests generate table-driven tests for this function
/setup-vscode configure editor settings for this repo
```

### 4) Verify

1. Reload VS Code window.
2. Open Copilot Chat.
3. Type `/` and confirm skills from this folder appear.

### Troubleshooting

- Skills do not appear: verify each skill folder contains `SKILL.md` and the frontmatter `name` matches the folder name.
- Wrong skills loaded: check for typos in `chat.agentSkillsLocations` paths and set unwanted locations to `false`.
- Still not loading: open Chat diagnostics and confirm the skill path is discovered.
