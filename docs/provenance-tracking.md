# Provenance Tracking

## Overview

Palimpsest tracks the complete lineage of prompts, from meta-prompts through generated prompts to their usage sessions. This enables understanding how prompts evolved and which meta-prompts are most effective.

## Tracking Levels

### 1. Generation Tracking
Tracks when meta-prompts generate other prompts:
- **Source**: Meta-prompt ID, version, and specific session
- **Generated**: Regular prompt or dev spec created
- **Artifacts**: Raw generation stored in session
- **Timing**: Exact timestamp of generation

### 2. Modification Tracking  
Tracks manual edits to generated prompts:
- **Original**: Link to source generation
- **Changes**: When manually edited
- **Editor**: Who made modifications
- **Reason**: Why modifications were needed

### 3. Usage Tracking
Tracks how prompts are used in practice:
- **Sessions**: All conversations using each prompt version
- **Performance**: Success rates and feedback
- **Evolution**: How usage drives new versions

## Storage Locations

### In Meta-Prompt Sessions
Generated artifacts stored in:
```
prompts/meta-prompts/{id}/sessions/generated-prompts/
├── regular-{id}-{timestamp}.txt
├── spec-{id}-{timestamp}.txt
└── ...
```

### In Generated Prompt Metadata
Source tracking in `metadata.toml`:
```toml
[provenance]
source_type = "meta-prompt"
source_id = "code-review-generator"
source_version = "v1.0.0"
source_session = "session-20250812-103000-v1.0.0"
generation_timestamp = "2025-08-12T10:35:00Z"
manually_edited = false
```

### In Global Index
Cross-references in `index/provenance.json`:
```json
{
  "relationships": [
    {
      "source": {
        "id": "code-review-generator",
        "type": "meta-prompt",
        "version": "v1.0.0",
        "session": "session-20250812-103000-v1.0.0"
      },
      "generated": [
        {
          "id": "react-component-reviewer",
          "type": "regular-prompt",
          "version": "v1.0.0",
          "timestamp": "2025-08-12T10:35:00Z",
          "manually_edited": false
        }
      ]
    }
  ]
}
```

## Workflow Example

### 1. Meta-Prompt Creation
```
User creates: prompts/meta-prompts/code-review-generator/versions/v1.0.0/
├── prompt.txt (the meta-prompt content)
├── metadata.toml (meta-prompt metadata)
└── authoring-conversation.jsonl (how it was created)
```

### 2. Generation Session
```
User runs session: prompts/meta-prompts/code-review-generator/sessions/
└── session-20250812-103000-v1.0.0.jsonl (conversation)

During session, artifacts created:
└── generated-prompts/
    └── regular-react-reviewer-20250812103500.txt
```

### 3. Prompt Finalization
```
Generated prompt copied to:
prompts/regular-prompts/react-component-reviewer/versions/v1.0.0/
├── prompt.txt (content from artifact)
├── metadata.toml (includes provenance section)
└── authoring-conversation.jsonl (copied from generation session)
```

### 4. Index Updates
- `prompts.json` updated with new regular prompt
- `provenance.json` updated with relationship
- `sessions.json` updated with generation session

## Query Capabilities

### Find All Generated Prompts
```bash
# From a meta-prompt
grep -r "source_id = \"code-review-generator\"" prompts/*/*/versions/*/metadata.toml
```

### Find Source of a Prompt
```bash
# For a specific prompt
cat prompts/regular-prompts/react-reviewer/versions/v1.0.0/metadata.toml | grep -A5 "\[provenance\]"
```

### Track Meta-Prompt Effectiveness
```bash
# Count generations per meta-prompt
jq '.relationships[].source.id' index/provenance.json | sort | uniq -c
```

## Benefits

### For Users
- **Understand Origins**: Know where each prompt came from
- **Track Evolution**: See how prompts improve over time
- **Find Related**: Discover similar prompts from same source
- **Assess Quality**: Evaluate meta-prompt effectiveness

### For Systems
- **Automated Cleanup**: Remove unused generated prompts
- **Performance Analysis**: Identify best-performing meta-prompts
- **Dependency Management**: Understand prompt relationships
- **Audit Trail**: Complete history of all changes

## Validation

### Consistency Checks
- All source references must exist
- Generation timestamps must be valid
- Session artifacts must match finalized prompts
- No circular dependencies

### Integrity Maintenance
- Orphaned prompts detection
- Missing provenance warnings
- Cross-reference validation
- Timestamp consistency checks