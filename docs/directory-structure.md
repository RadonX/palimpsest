# Directory Structure

## Complete Layout

```
palimpsest/
├── docs/                              # Project documentation
│   ├── README.md
│   ├── directory-structure.md
│   ├── asset-versioning-guide.md
│   ├── usage-guide.md
│   └── slash-command-workflow.md
├── prompts/
│   ├── slash-commands/
│   │   └── {command-id}/
│   │       ├── latest.md              # Symlink to current version
│   │       ├── sessions/
│   │       │   └── session-{timestamp}-{version}.jsonl
│   │       └── versions/
│   │           ├── v1.0.0/
│   │           │   ├── command.md
│   │           │   └── metadata.toml
│   │           └── v1.1.0/
│   │               ├── command.md
│   │               └── metadata.toml
│   └── output-style/
│       └── {style-id}/
│           ├── latest.md              # Symlink to current version
│           ├── sessions/
│           │   └── session-{timestamp}-{version}.jsonl
│           └── versions/
│               ├── v1.0.0/
│               │   ├── system_prompt.md
│               │   └── metadata.toml
│               └── v1.1.0/
│                   ├── system_prompt.md
│                   └── metadata.toml
└── templates/
    └── metadata-template.toml
```

## Directory Purposes

### `/prompts/slash-commands/`
Interactive commands for Claude Code. Markdown format with frontmatter metadata.

### `/prompts/output-style/`
System prompt modifications that change Claude's behavior while maintaining core capabilities.

### `/prompts/{type}/{id}/versions/`
- Immutable versions using semantic versioning
- Each version contains: content file + metadata.toml
- Never modify existing versions

### `/prompts/{type}/{id}/sessions/`
- Conversation logs using each version
- JSONL format with version suffix

### `/templates/`
Boilerplate files for creating new assets.

## Naming Conventions

### Asset IDs
- Kebab-case: `code-review`, `explanatory`
- Descriptive and unique
- No version info in ID

### Session Files
- Format: `session-{timestamp}-{version}.jsonl`
- Example: `session-20250812-103000-v1.0.0.jsonl`
- Timestamp: YYYYMMDD-HHMMSS format