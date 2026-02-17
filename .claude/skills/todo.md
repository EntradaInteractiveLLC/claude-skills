---
name: todo
description: "Write deferred tasks, bugs, tech debt, and follow-up items to a project-specific TODO.md so future sessions have full context without needing conversation history. Use when: (1) encountering a bug or issue that is out of scope for the current task, (2) the user says things like 'note this for later', 'add this to the TODO', 'we will fix that later', 'remember to...', (3) discovering tech debt or a missing feature during implementation, (4) a task is intentionally deferred or descoped. Always write to TODO.md in the project root directory."
---

# Todo

Write deferred items to `TODO.md` in the project root so future sessions can pick them up without conversation history.

## When to Trigger

Trigger automatically (without being asked) when:
- Discovering a bug or issue that is out of scope for the current task
- Finding tech debt, a code smell, or a missing feature during implementation
- A subtask is explicitly descoped or punted ("we'll come back to that")
- The user says anything like: "note this", "remember this", "add to TODO", "we should fix X later"

Also trigger when the user explicitly invokes `/todo`.

## TODO.md Location

Always write to the **project root** — same directory as `CLAUDE.md` or equivalent project config file.

If there is no clear project root, ask the user once, then remember it for the session.

## File Header (write once, at top of file)

If TODO.md does not exist or has no header, prepend this block:

```markdown
# TODO

Items deferred for future sessions. Each entry is self-contained — written with enough context that a new session can act on it without knowing the conversation history it came from.

> **Priorities**: `HIGH` = blocks progress or causes incorrect behavior | `MED` = should be done soon | `LOW` = nice to have

---

```

## Item Template

Append each new item using this exact format:

```markdown
### [PRIORITY] <Short imperative title>

- **Area**: <System/domain — e.g., Mass AI, UI, Weapons, Networking, PlayFab>
- **Discovered**: <YYYY-MM-DD>
- **Context**: <1-2 sentences: what were we working on, what led to finding this?>
- **Problem / Task**: <Specific description of what needs to be done. Be concrete — file names, function names, observed behavior, expected behavior.>
- **Location**: <File path(s), line numbers, Blueprint asset paths, or "N/A">
- **Why deferred**: <Why not fixed now? e.g., "Out of scope for sprint", "Requires refactor", "Needs design decision">
- **Approach**: <Optional — suggested fix, relevant pattern, or known gotcha>

---

```

## Priority Guidelines

| Priority | Use When |
|----------|----------|
| `HIGH` | Bug that causes incorrect behavior, blocks a feature, or will cause problems if ignored |
| `MED` | Tech debt, missing validation, suboptimal pattern that should be cleaned up soon |
| `LOW` | Nice-to-have improvement, cosmetic issue, future optimization |

## Behavior Rules

1. **Always use the template** — never write freeform notes. Future sessions depend on the structure.
2. **Be specific in Problem / Task** — vague entries are useless. Name the file, function, and exact symptom.
3. **Don't truncate context** — include enough detail that a cold session can act without re-investigation.
4. **Check before appending** — if TODO.md exists, read it first to avoid duplicating an already-tracked item.
5. **Confirm to the user** — after writing, say: "Added to TODO.md: [title]" so they know it was captured.
6. **Do not resolve items** — only mark items done if the user explicitly says the issue is fixed.

## Resolving / Removing Items

When a TODO item is completed in a session:
- Remove the item from TODO.md (or strike it through with `~~title~~` if the user prefers to keep history)
- Confirm to the user: "Removed from TODO.md: [title]"
