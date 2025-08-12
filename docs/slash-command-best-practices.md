# Slash Command Best Practices

## Overview

Based on research from Claude Code documentation and community best practices, this guide provides recommendations for creating effective slash commands within the Palimpsest system.

## Frontmatter Standards

### Frontmatter Structure
See `templates/slash-command-template.md` for the complete frontmatter structure. Key fields include:

- **allowed-tools**: Tools Claude can use (Read, Write, Edit, Bash, etc.)
- **description**: Brief command description
- **argument-hint**: User guidance for arguments
- **model**: Claude model to use (sonnet, opus, haiku)

## Tool Specifications

### Common Tool Patterns
- **File Operations**: `Read(*)`, `Write(*)`, `Edit(*)`
- **Search Operations**: `LS(*)`, `Glob(*)`, `Grep(*)`
- **Git Operations**: `Bash(git:*)`
- **GitHub CLI**: `Bash(gh:*)`
- **Web Operations**: `WebFetch(*)`, `WebSearch(*)`
- **Directory Operations**: `Bash(mkdir:*)`, `Bash(ls:*)`

### Tool Specificity
- Use specific patterns when possible: `Bash(git add:*)` instead of `Bash(*)`
- Only include tools actually needed by the command
- Consider security implications of broad tool access

## Argument Handling

### Using $ARGUMENTS
Reference the template for $ARGUMENTS usage patterns. Key points:
- Use `$ARGUMENTS` to access all provided arguments
- Parse arguments within your command logic
- Validate inputs appropriately

### Argument Hints
- Provide clear guidance: `"[file-pattern] [options]"`
- Use square brackets for optional: `"<required> [optional]"`
- Include examples: `"issue-number" for GitHub issues`

## Command Structure

### Naming Conventions
- Use kebab-case for command names: `review-code`, `create-component`
- Keep names short but descriptive
- Consider namespace organization: `frontend/component`, `git/commit`

### Content Organization
Follow the structure in `templates/slash-command-template.md`:
- Clear command title
- Brief description
- Argument usage explanation
- Process steps
- Usage examples

## Model Selection

### Model Guidelines
- **Haiku**: Simple, fast commands (text processing, formatting)
- **Sonnet**: Balanced commands (code review, analysis)
- **Opus**: Complex commands (architectural decisions, comprehensive analysis)

## Scope and Deployment

### Project vs User Commands
- **Project Commands**: Team-shared, in `.claude/commands/`
- **User Commands**: Personal, in `~/.claude/commands/`
- Specify `scope = "project"` or `scope = "user"` in metadata

### Namespace Organization
```
frontend/
├── component.md
├── page.md
└── test.md

backend/
├── api.md
├── database.md
└── service.md
```

## Security Considerations

### Tool Restrictions
- Limit bash commands to specific operations
- Avoid broad file system access unless necessary
- Be cautious with web operations and external APIs

### Input Validation
- Include validation logic in command content
- Handle malformed arguments gracefully
- Sanitize inputs when used in bash commands

## Version Management

### Changelog Tracking
Document changes in metadata.toml:
```toml
[[changelog.entries]]
version = "2.0.0"
date = "2025-08-12"
changes = ["Added argument validation", "Improved error handling"]
```

### Semantic Versioning
- **Major**: Breaking changes to command interface
- **Minor**: New features, backward compatible
- **Patch**: Bug fixes, improvements

## Community Patterns

### Common Command Types
1. **Code Review**: Analysis and feedback on code
2. **File Generation**: Create boilerplate files/components
3. **Git Operations**: Automated git workflows
4. **Documentation**: Generate or update docs
5. **Testing**: Run and analyze tests

### Reusable Components
- Create focused, single-purpose commands
- Design for composition with other commands
- Include clear success/failure indicators

## Integration with Palimpsest

### Metadata Alignment
Ensure command metadata.toml includes:
- Proper `[command]` section instead of `[prompt]`
- `[frontmatter]` section preserving original Claude Code settings
- `[changelog]` for version tracking
- Appropriate `[tags]` for organization

### Provenance Tracking
- Link generated commands to source meta-prompts
- Maintain audit trail of command evolution
- Track external sources and adaptations

## Testing and Validation

### Before Deployment
- Test command with various argument patterns
- Verify tool permissions work as expected
- Check argument-hint accuracy
- Validate description clarity

### Continuous Improvement
- Monitor command usage and effectiveness
- Collect feedback from team members
- Update based on evolving requirements
- Maintain version history for rollback capability