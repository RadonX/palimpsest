# Provenance Tracking

## Overview

Palimpsest tracks the lineage and usage of slash commands and output styles to understand their evolution and effectiveness.

## Tracking Levels

### 1. Creation Tracking
- **Author**: Who created the asset
- **Source**: External source or original creation
- **Timing**: When each version was created

### 2. Modification Tracking  
- **Versions**: Complete version history
- **Changes**: Changelog entries for each version
- **Editor**: Who made modifications
- **Reason**: Why modifications were needed

### 3. Usage Tracking
- **Sessions**: All conversations using each version
- **Performance**: Usage patterns and feedback

## Storage Locations

### In Asset Metadata
Version tracking in `metadata.toml`:
```toml
[command]  # or [output_style]
version = "v1.1.0"
created = "2025-08-17T00:00:00Z"
updated = "2025-08-17T12:00:00Z"

[author]
name = "author-name"

[source]
type = "external"  # or "original"
url = "https://github.com/user/repo"
original_author = "original-author"

[[changelog.entries]]
version = "v1.1.0"
date = "2025-08-17"
changes = ["Fixed quotes", "Added missing content"]

[lineage]
deprecated = false
```

### In Sessions
Usage tracking in session files:
```
prompts/slash-commands/{id}/sessions/session-{timestamp}-{version}.jsonl
prompts/output-style/{id}/sessions/session-{timestamp}-{version}.jsonl
```

## Query Capabilities

### Find Usage
```bash
# Find all sessions for an asset
ls prompts/slash-commands/my-command/sessions/

# Find sessions for specific version
ls prompts/*/my-asset/sessions/*v1.0.0.jsonl
```

### Track Evolution
```bash
# View version history
ls prompts/slash-commands/my-command/versions/

# View changelog
grep -A10 "changelog" prompts/*/my-asset/versions/*/metadata.toml
```

## Benefits

- **Understand Origins**: Know where each asset came from
- **Track Evolution**: See how assets improve over time  
- **Assess Usage**: Evaluate asset effectiveness
- **Audit Trail**: Complete history of all changes