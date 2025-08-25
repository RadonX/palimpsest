# Palimpsest Project Agreement

## Purpose

A filesystem-only layout for storing meta prompts, the single conversation that authored each version of a meta prompt, and unlimited generated sessions created by that version.

## Core Principles

### 1. Filesystem-Based Storage
- All data stored as files and directories
- No database dependencies
- Human-readable formats (TOML, TXT, JSONL)
- Version control friendly structure

### 2. Prompt Type Hierarchy
- **Meta-prompts**: Generate other prompts
- **Regular prompts**: Standard prompts for specific tasks  

- **Slash commands**: Interactive Claude Code commands with frontmatter
- **Agents.md Instructions**: Versioned instructions for AI coding agents (agents.md)
- **Sub-Agents**: Specialized AI assistants for task delegation
- **Extensible**: Support for additional prompt types

### 3. Complete Provenance Tracking
- Track which meta-prompt generated each regular prompt
- Store the exact session that created each generated prompt
- Maintain lineage across prompt versions
- Support manual editing of generated prompts
- Track external sources with proper attribution
- Support adapted prompts from external repositories

### 4. Version Management
- Semantic versioning for all prompts
- Immutable versions (no overwriting)
- Single authoring conversation per version
- Clear version lineage and change tracking

### 5. Session Management
- All conversations stored as JSONL files
- Sessions linked to specific prompt versions
- Generated artifacts tracked within sessions
- Unlimited sessions per prompt version

## Key Decisions

### File Formats
- **TOML**: Configuration and metadata files (human-readable)
- **TXT**: Prompt content (plain text)
- **Markdown**: Slash commands with YAML frontmatter (Claude Code compatible)
- **JSONL**: Conversations and sessions (streaming, appendable)
- **JSON**: Index files and structured data

### Directory Organization
- Sessions stored at prompt level (not nested under versions)
- Generated prompts stored in both session artifacts and target type directories
- Separate index files for fast lookups
- Templates directory for prompt creation

### Provenance System
- Generated prompts reference source meta-prompt in metadata
- Session artifacts preserved in meta-prompt sessions
- Bidirectional tracking in provenance.json
- Support for manual editing tracking
- External source attribution with URL and author tracking
- Adaptation notes for modified external content

## Non-Goals

- Real-time collaboration
- Complex query capabilities
- Web interface (filesystem tools sufficient)
- Database-style transactions