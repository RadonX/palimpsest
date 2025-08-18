# Output Style Guide

## What are Output Styles?

Output styles are system prompt modifications that completely transform how Claude Code behaves. Unlike other Claude Code features that add to or modify the default prompt, output styles completely replace the system prompt with custom instructions while preserving core tool capabilities.

## Key Characteristics

- **Complete system prompt replacement** (not additive like CLAUDE.md or --append-system-prompt)
- **Core capabilities maintained** (file operations, tool access, task management)
- **Project-level persistence** (saved in `.claude/settings.local.json`)

## Content Structure

Output styles contain a system prompt with optional frontmatter:

```markdown
---
name: Style Name
description: Brief description of the style
---

[System prompt content that completely replaces Claude Code's default behavior]
```

## Differences from Other Asset Types

| Feature | Output Styles | Slash Commands | CLAUDE.md |
|---------|---------------|----------------|-----------|
| Scope | Complete behavior change | Single interaction | Context addition |
| Persistence | Project-level | Per-invocation | Per-project |
| System Prompt | Replaces entirely | Unchanged | Adds user message |
| Activation | `/output-style name` | `/command` | Automatic |