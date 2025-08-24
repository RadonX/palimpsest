# Asset Versioning Guide

## Rules
1. **Never modify existing versions** - always create new version directories
2. **Metadata.toml per version** - each version has its own metadata file
3. **Semantic versioning**: v1.0.0 format
4. **latest.md symlink** - always points to current version in root directory

## Structure
```
asset-name/
├── latest.md                  # Symlink to current version
├── sessions/                  # Conversation logs (slash commands only)
└── versions/
    ├── v1.0.0/
    │   ├── command.md        # or system_prompt.md for output-styles, agent.md for sub-agents
    │   └── metadata.toml     # Version-specific metadata
    └── v1.1.0/
        ├── command.md
        └── metadata.toml
```

## Create New Version

```bash
# 1. Create directory (adjust path for asset type)
mkdir -p prompts/slash-commands/my-command/versions/v1.1.0        # slash commands
mkdir -p prompts/output-style/my-style/versions/v1.1.0            # output styles
mkdir -p prompts/sub-agent/my-agent/versions/v1.1.0               # sub-agents

# 2. Copy previous version
cp versions/v1.0.0/command.md versions/v1.1.0/command.md          # slash commands
cp versions/v1.0.0/system_prompt.md versions/v1.1.0/system_prompt.md  # output styles
cp versions/v1.0.0/agent.md versions/v1.1.0/agent.md              # sub-agents
cp versions/v1.0.0/metadata.toml versions/v1.1.0/metadata.toml    # copy metadata

# 3. Edit new version - make your changes

# 4. Update metadata.toml - version field and changelog entry

# 5. Update latest.md symlink
rm latest.md && ln -sf versions/v1.1.0/command.md latest.md       # slash commands
rm latest.md && ln -sf versions/v1.1.0/system_prompt.md latest.md # output styles
rm latest.md && ln -sf versions/v1.1.0/agent.md latest.md         # sub-agents
```

### Metadata Update
```toml
[command]           # or [output_style] for output styles, [sub_agent] for sub-agents
version = "v1.1.0"
updated = "2025-08-16T12:00:00Z"

[[changelog.entries]]
version = "v1.1.0"
date = "2025-08-16"
changes = ["Fixed quotes", "Added missing content", "Removed redundancy"]
```

## Semantic Versioning

- **v2.0.0 (Major)**: Breaking changes (arguments, behavior, tools)
- **v1.1.0 (Minor)**: New features, quote fixes, improvements
- **v1.0.1 (Patch)**: Typos, small fixes

## Fix Accidental Edits

```bash
# Restore from git
git checkout HEAD -- prompts/slash-commands/command-name/versions/v1.0.0/command.md

# Fix broken latest.md symlink
cd prompts/slash-commands/command-name
rm latest.md && ln -sf versions/v1.0.0/command.md latest.md
```

## Asset Types

### Slash Commands
- **Location**: `prompts/slash-commands/`
- **File**: `command.md` 
- **Metadata**: `[command]` section
- **Usage**: Executable commands via `/command-name`

### Output Styles  
- **Location**: `prompts/output-style/`
- **File**: `system_prompt.md`
- **Metadata**: `[output_style]` section
- **Usage**: System prompt modifications via `/output-style style-name`

### Sub-Agents
- **Location**: `prompts/sub-agent/`
- **File**: `agent.md` (with YAML frontmatter)
- **Metadata**: `[sub_agent]` section
- **Usage**: Specialized AI assistants via Task tool delegation
- **Features**: Context isolation, tool restrictions, domain expertise