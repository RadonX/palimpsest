# Slash Command Workflow

## Setup Process
For version creation, see [Asset Versioning Guide](asset-versioning-guide.md).

### Slash Command Specific Steps

**1. Create sessions directory**
```bash
mkdir -p prompts/slash-commands/{command-name}/sessions
```

**2. Create symbolic links**
```bash
# Version management link
ln -s v{X.Y.Z}/command.md prompts/slash-commands/{command-name}/versions/latest.md

# Claude Code deployment link  
ln -s ../../prompts/slash-commands/{command-name}/versions/latest.md .claude/commands/{command-name}.md
```

### Link Chain
1. **latest.md** → points to current version
2. **.claude/commands/{name}.md** → points to latest.md
3. **Result**: Claude Code auto-discovers commands and uses current version

### Verification
```bash
# Check links work
ls -la .claude/commands/{command-name}.md
cat .claude/commands/{command-name}.md  # Should show command content
```

### Update Version
```bash
# Update latest.md to point to new version
rm prompts/slash-commands/{command-name}/versions/latest.md
ln -s v{X.Y.Z}/command.md prompts/slash-commands/{command-name}/versions/latest.md
# Claude Code automatically uses new version
```