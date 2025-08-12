# File Format Specifications

## Overview

Palimpsest uses four primary file formats:
- **TOML**: Human-readable configuration and metadata
- **TXT**: Plain text content for prompts and specifications  
- **JSONL**: Streaming conversations and sessions
- **JSON**: Structured index and lookup data

## TOML Files

### Purpose
- Configuration files (`palimpsest.toml`)
- Metadata files (`metadata.toml`)
- Template definitions
- Schema specifications

### Advantages
- Human-readable and editable
- Supports nested structures
- Comments allowed
- Git-friendly diffs

### File Extensions
- `.toml` for all TOML files

## TXT and Markdown Files

### Purpose
- Prompt content (`prompt.txt`)
- Specification content (`spec.txt`)
- Slash command content (`command.md`)
- Template content
- Any plain text artifacts

### Format
- UTF-8 encoding
- Line endings: platform native
- No length restrictions
- Markdown formatting allowed

### File Extensions
- `.txt` for prompt/spec content
- `.md` for slash commands and documentation

## JSONL Files

### Purpose
- Conversation logs (`authoring-conversation.jsonl`)
- Session recordings (`session-*.jsonl`)
- Any streaming/appendable data

### Format
- One complete JSON object per line
- UTF-8 encoding
- No trailing commas
- Each line is valid JSON

### Message Schema
```jsonl
{"role": "system|user|assistant", "content": "message text", "timestamp": "ISO8601", "message_id": "unique_id", "artifacts": []}
```

### Advantages
- Streamable and appendable
- Easy to process line-by-line
- Robust against partial reads
- Efficient for large conversations

### File Extensions
- `.jsonl` for all line-delimited JSON

## JSON Files

### Purpose
- Index files (`prompts.json`, `sessions.json`, etc.)
- Structured lookup data
- Cross-reference tables
- Summary information

### Format
- Pretty-printed with 2-space indentation
- UTF-8 encoding
- Complete JSON documents (not streaming)

### Advantages
- Fast parsing for lookups
- Rich structure support
- Tool ecosystem support
- Schema validation possible

### File Extensions
- `.json` for all JSON files

## Markdown Files (Slash Commands)

### Purpose
- Slash command definitions (`command.md`)
- Support YAML frontmatter for metadata
- Interactive Claude Code commands
- Quick development workflows

### Format
```markdown
---
tools_allowed: [read, write]
extended_thinking: false
---

# Command content here
```

### Advantages
- Frontmatter for command configuration
- Rich markdown formatting
- Compatible with Claude Code
- Human-readable and editable

### File Extensions
- `.md` for slash command files

## Character Encoding

All files use **UTF-8** encoding to support international characters and emojis in prompts and conversations.

## Line Endings

- **TOML/TXT/Markdown/JSON**: Platform native line endings
- **JSONL**: LF (`\n`) only for cross-platform consistency

## File Size Considerations

- **TOML/TXT/Markdown**: No practical limits
- **JSONL**: Designed for large files, process streaming
- **JSON**: Keep index files reasonable (<10MB recommended)

## Validation

### TOML Files
- Must parse without errors
- Required fields per schema
- Valid semantic versions

### Markdown Files
- Valid YAML frontmatter (if present)
- Markdown syntax compliance
- Required frontmatter fields for slash commands

### JSONL Files
- Each line must be valid JSON
- Required message fields present
- Valid ISO8601 timestamps

### JSON Files
- Valid JSON structure
- Schema compliance for index files
- Consistent ID references