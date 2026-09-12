---
title: Choosing an Install Scope for Claude Code Plugins and Skills
---

When you install a plugin or skill in Claude Code, it asks where to store that choice:

- Install for you (**user scope**)
- Install for all collaborators on this repository (**project scope**)
- Install for you, in this repo only (**local scope**)

Each option writes to a different file, which determines who sees the plugin and whether it's tracked in git.

## User scope

**File:** `~/.claude/settings.json`

Lives in your home directory, outside any repository. The plugin becomes available in every project you open on this machine, and nothing gets written to the repo.

Use this for plugins you personally want everywhere — general-purpose tools, not tied to one codebase.

## Project scope

**File:** `.claude/settings.json` (in the repo root)

Committed to git. Anyone who clones the repo gets the plugin automatically when they open it in Claude Code.

Use this for plugins the whole team should have — shared conventions, project-specific commands, standards everyone should follow.

## Local scope

**File:** `.claude/settings.local.json`

Scoped to this repo, but not committed. Claude Code adds `**/.claude/settings.local.json` to your global git excludes the first time it writes the file, so it won't show up as untracked either.

Use this when you want a plugin active in one specific project, but it's a personal preference rather than a team standard — or you're just trying something out before proposing it for project scope.

## How they stack

All three scopes store enabled plugins the same way, under an `enabledPlugins` key — there's no separate marketplace config file. If the same plugin is set at more than one scope, precedence runs:

```
command line > local (.claude/settings.local.json) > project (.claude/settings.json) > user (~/.claude/settings.json)
```

So a local override always beats the shared project setting, and the project setting always beats your personal user-wide default.

## Rule of thumb

- **Solo tool you want everywhere** → user scope
- **Team standard for this project** → project scope
- **Personal tweak for this project only** → local scope
