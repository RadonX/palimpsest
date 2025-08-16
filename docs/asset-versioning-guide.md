# Asset Versioning Guide

## Rules
1. **Never modify existing versions** - always create new version directories
2. **Single metadata.toml** per asset (not per version)
3. **Semantic versioning**: v1.0.0 format

## Structure
```
asset-name/
├── metadata.toml              # Central version management
├── sessions/                  # Conversation logs (slash commands only)
└── versions/
    ├── latest.md             # Current version
    ├── v1.0.0/
    │   └── command.md        # or prompt.md
    └── v1.1.0/
        └── command.md
```

## Create New Version

```bash
# 1. Create directory (adjust path for asset type)
mkdir -p prompts/slash-commands/my-command/versions/v1.1.0        # slash commands
mkdir -p prompts/meta-prompts/my-prompt/versions/v1.1.0           # meta-prompts  
mkdir -p prompts/regular-prompts/my-prompt/versions/v1.1.0        # regular prompts

# 2. Copy previous version
cp versions/v1.0.0/command.md versions/v1.1.0/command.md          # slash commands
cp versions/v1.0.0/prompt.md versions/v1.1.0/prompt.md            # prompts

# 3. Edit new version - make your changes

# 4. Update metadata.toml - version field and changelog entry
```

### Metadata Update
```toml
[command]           # or [prompt] for prompts
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
```