# claude-skills

A collection of Claude Code skills built by [Entrada Interactive](https://github.com/EntradaInteractiveLLC).

## What are Claude Skills?

Skills are reusable prompt templates that extend Claude Code with specialized workflows. They're invoked with a `/skill-name` slash command inside Claude Code.

## Installation

### Install a single skill

Copy the desired skill's folder into your project's `.claude/skills/` directory:

```bash
# From your project root
mkdir -p .claude/skills/skill-name
cp path/to/claude-skills/.claude/skills/skill-name/SKILL.md .claude/skills/skill-name/SKILL.md
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
| `todo` | Writes deferred tasks, bugs, and tech debt to `TODO.md` so future sessions have full context |
| `step-back` | Breaks debugging doom loops — generates 5 ranked hypotheses before touching any code |

