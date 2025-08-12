---
allowed-tools: [Read(*), Write(*), Edit(*)]
argument-hint: "[optional arguments]"
description: "Brief description of what this command does"
model: sonnet
---

# Command Name

Write your slash command prompt content here. This will be executed when the command is invoked.

## Arguments

You can reference arguments in your prompt using `$ARGUMENTS`:
- Use `$ARGUMENTS` to access all provided arguments
- Parse arguments within your prompt logic

## File Context

Reference files using `@filename` syntax in Claude Code, or specify file_patterns in metadata.toml for automatic context inclusion.

## Bash Commands

Use `!command` syntax for bash commands (if allowed-tools includes Bash).

## Example Usage

```
/your-command [arguments]
```

## Best Practices

- Keep commands focused on a single task
- Use clear, descriptive names
- Specify minimal required allowed-tools
- Include helpful argument hints
- Consider namespace organization for related commands