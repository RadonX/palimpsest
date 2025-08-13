# Slash Command Workflow

## Complete Slash Command Setup Process

This document outlines the complete workflow for adding new slash commands to the palimpsest repository with full version management and Claude Code integration.

### Required Steps for Every Slash Command

**1. Directory Structure**
```bash
# Create full directory structure
mkdir -p prompts/slash-commands/{command-name}/versions/v{X.Y.Z}
mkdir -p prompts/slash-commands/{command-name}/sessions
```

**2. Command File**
```bash
# Copy command content to proper location
cp source/command.md prompts/slash-commands/{command-name}/versions/v{X.Y.Z}/command.md
```

**3. Metadata File**
```bash
# Create metadata following our schema
# Edit metadata.toml with appropriate [command], [author], [usage], [behavior], and [source] sections
```

**4. Symbolic Links (CRITICAL)**
```bash
# Create version management link
ln -s v{X.Y.Z}/command.md prompts/slash-commands/{command-name}/versions/latest.md

# Create Claude Code deployment link
ln -s ../../prompts/slash-commands/{command-name}/versions/latest.md .claude/commands/{command-name}.md
```

### Link Structure Explanation

The two-level symbolic linking provides:

**Level 1: Version Management**
- `latest.md → v{X.Y.Z}/command.md`
- Points to current active version
- Easy to update when new versions are released

**Level 2: Claude Code Integration**  
- `.claude/commands/{name}.md → ../../prompts/slash-commands/{name}/versions/latest.md`
- Makes commands discoverable by Claude Code
- Automatically uses current version through latest.md

### Benefits

1. **Version Control**: Full history preserved, easy version switching
2. **Claude Code Integration**: Commands automatically available in `/help`
3. **Update Simplicity**: New versions only require updating one symbolic link
4. **Consistency**: Same pattern across all commands
5. **Traceability**: Complete provenance and changelog tracking

### Verification Commands

```bash
# Check symbolic links are created correctly
ls -la prompts/slash-commands/{command-name}/versions/latest.md
ls -la .claude/commands/{command-name}.md

# Verify command is discoverable
find .claude/commands/ -name "*.md" -type l

# Test link chain works
cat .claude/commands/{command-name}.md  # Should show command content
```

### Common Mistakes to Avoid

- **Missing sessions directory**: Always create both versions/ and sessions/
- **Forgetting symbolic links**: Commands won't work in Claude Code without .claude/commands/ links
- **Wrong link paths**: Use relative paths for portability
- **Incomplete metadata**: Follow schema exactly, omit empty optional fields
- **Version format**: Always use semantic versioning (v1.0.0, not 1.0.0)

### Update Workflow for New Versions

```bash
# 1. Create new version directory
mkdir -p prompts/slash-commands/{command-name}/versions/v{X.Y.Z}

# 2. Add new command file and metadata
cp new-command.md prompts/slash-commands/{command-name}/versions/v{X.Y.Z}/command.md
# Create new metadata.toml with updated version and changelog

# 3. Update symbolic link to point to new version
rm prompts/slash-commands/{command-name}/versions/latest.md
ln -s v{X.Y.Z}/command.md prompts/slash-commands/{command-name}/versions/latest.md

# Claude Code link automatically uses new version through latest.md
```

This workflow ensures all slash commands follow consistent patterns and integrate properly with both the palimpsest versioning system and Claude Code.