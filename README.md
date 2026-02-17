# claude-skills

A collection of Claude Code skills built by [Entrada Interactive](https://github.com/EntradaInteractiveLLC).

## What are Claude Skills?

Skills are reusable prompt templates that extend Claude Code with specialized workflows. They're invoked with a `/skill-name` slash command inside Claude Code.

## Installation

### Install a single skill

Copy the desired `.md` file from `.claude/skills/` into your project's `.claude/skills/` folder:

```bash
# From your project root
mkdir -p .claude/skills
cp path/to/claude-skills/.claude/skills/skill-name.md .claude/skills/
```

### Install all skills globally

Copy the entire `.claude/skills/` folder into your global Claude config:

```bash
# Windows
cp -r path/to/claude-skills/.claude/skills/. "$USERPROFILE/.claude/skills/"

# macOS / Linux
cp -r path/to/claude-skills/.claude/skills/. ~/.claude/skills/
```

## Skills

| Skill | Description |
|-------|-------------|
| *(coming soon)* | |

## Docs

See the [`docs/`](./docs/) folder for guides on usage and how to write your own skills.
