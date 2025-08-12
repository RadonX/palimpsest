# Directory Structure

## Complete Layout

```
palimpsest/
├── palimpsest.toml                    # Global configuration
├── docs/                              # Project documentation
│   ├── README.md
│   ├── project-agreement.md
│   ├── directory-structure.md
│   ├── file-formats.md
│   ├── metadata-schemas.md
│   ├── usage-guide.md
│   └── provenance-tracking.md
├── prompts/
│   ├── meta-prompts/
│   │   └── {prompt-id}/
│   │       ├── versions/
│   │       │   ├── v1.0.0/
│   │       │   │   ├── prompt.txt
│   │       │   │   ├── metadata.toml
│   │       │   │   └── authoring-conversation.jsonl
│   │       │   └── v1.1.0/
│   │       │       ├── prompt.txt
│   │       │       ├── metadata.toml
│   │       │       └── authoring-conversation.jsonl
│   │       └── sessions/
│   │           ├── session-{timestamp}-v1.0.0.jsonl
│   │           ├── session-{timestamp}-v1.0.0.jsonl
│   │           ├── session-{timestamp}-v1.1.0.jsonl
│   │           └── generated-prompts/          # Prompts created by this meta-prompt
│   │               ├── regular-{id}-{timestamp}.txt
│   │               └── spec-{id}-{timestamp}.txt
│   ├── regular-prompts/
│   │   └── {prompt-id}/
│   │       ├── versions/
│   │       │   ├── v1.0.0/
│   │       │   │   ├── prompt.txt
│   │       │   │   ├── metadata.toml          # Includes source_meta_prompt if generated
│   │       │   │   └── authoring-conversation.jsonl
│   │       │   └── v1.1.0/
│   │       └── sessions/
│   │           └── session-{timestamp}-v1.0.0.jsonl
│   ├── dev-specs/
│   │   └── {spec-id}/
│   │       ├── versions/
│   │       │   ├── v1.0.0/
│   │       │   │   ├── spec.txt
│   │       │   │   ├── metadata.toml
│   │       │   │   └── authoring-conversation.jsonl
│   │       │   └── v1.1.0/
│   │       └── sessions/
│   └── {other-prompt-types}/
├── templates/
│   ├── meta-prompt-template.txt
│   ├── regular-prompt-template.txt
│   ├── dev-spec-template.txt
│   └── metadata-template.toml
└── index/
    ├── prompts.json                   # All prompts with type and provenance
    ├── sessions.json
    ├── provenance.json                # Meta-prompt → generated prompt relationships
    └── tags.json
```

## Directory Purposes

### `/prompts/`
Main storage for all prompt types, organized by type then by prompt ID.

### `/prompts/{type}/{prompt-id}/versions/`
- Immutable versions of each prompt
- Each version contains: content file, metadata, authoring conversation
- Semantic versioning (v1.0.0, v1.1.0, etc.)

### `/prompts/{type}/{prompt-id}/sessions/`
- All sessions using this prompt
- Session filenames include version suffix
- Contains actual conversations with users/systems

### `/prompts/meta-prompts/{id}/sessions/generated-prompts/`
- Artifacts created during meta-prompt sessions
- Raw generated content before being processed into typed prompts
- Maintains original generation context

### `/templates/`
- Boilerplate files for creating new prompts
- Schema templates for metadata
- Starting points for different prompt types

### `/index/`
- Fast lookup files
- Cross-references and relationships
- Tag-based organization
- Session summaries

### `/docs/`
- Project documentation
- Specifications and agreements
- Usage guides and examples

## Naming Conventions

### Prompt IDs
- Kebab-case: `code-review-generator`
- Descriptive and unique across all types
- No version info in ID (versions are separate)

### Session Files
- Format: `session-{timestamp}-{version}.jsonl`
- Example: `session-20250812-103000-v1.0.0.jsonl`
- Timestamp: YYYYMMDD-HHMMSS format

### Generated Artifacts
- Format: `{type}-{id}-{timestamp}.txt`
- Example: `regular-react-reviewer-20250812103500.txt`
- Links to source session via timestamp