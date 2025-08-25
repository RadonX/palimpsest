# Metadata Schemas

This document defines the structure of `metadata.toml` files used in Palimpsest.

## Common Asset Metadata

All asset types share the following common metadata fields and sections.

### Core Attributes

These attributes are required for every asset type and are defined in the main table of the asset (e.g., `[prompt]`, `[command]`).

-   `id`: Unique identifier for the asset (string, required).
-   `type`: The type of the asset (string, required).
-   `title`: Human-readable title (string, required).
-   `description`: A brief description of the asset's purpose (string, required).
-   `version`: Semantic version string, e.g., "v1.0.0" (string, required).
-   `created`: ISO 8601 timestamp of when the asset was created (datetime, required).
-   `updated`: ISO 8601 timestamp of the last modification (datetime, required).

### Common Sections

The following sections are common to most asset types.

```toml
[author]
name = "string"                  # Required: Author name
email = "string"                 # Optional: Author email
organization = "string"          # Optional: Organization/team

[tags]
categories = ["string"]          # Required: At least one category
domains = ["string"]             # Optional: Domain/subject areas

[lineage]
parent_version = "string"        # Optional: Previous version
deprecated = false               # Optional: Default false

[changelog]
# Version history tracking
[[changelog.entries]]
version = "string"               # Version number
date = "datetime"                # Release date
changes = ["string"]             # List of changes made
```

## Asset-Specific Schemas

The following sections define the schemas for each asset type. They include the common metadata fields and any additional fields specific to that asset type.

---

### Meta-Prompt Schema

A prompt that generates other prompts.

```toml
[prompt]
# Includes all Core Attributes.
type = "meta-prompt"

[author]
# Includes the common [author] section.

[generation]
target_types = ["string"]        # Required: What this meta-prompt generates
expected_outputs = ["string"]    # Optional: Expected output categories

[tags]
# Includes the common [tags] section.
difficulty = "string"            # Optional: beginner|intermediate|advanced

[performance]
usage_count = 0                  # Optional: Number of times used
success_rate = 0.0               # Optional: Success rate (0.0-1.0)
avg_generation_time = 0.0        # Optional: Average time in seconds

[lineage]
# Includes the common [lineage] section.
```

---

### Regular Prompt Schema

A standard prompt for a specific task.

```toml
[prompt]
# Includes all Core Attributes.
type = "regular-prompt"

[author]
# Includes the common [author] section.

[provenance]
source_type = "string"           # Optional: "meta-prompt" if generated
source_id = "string"             # Optional: Source meta-prompt ID
source_version = "string"        # Optional: Source version
source_session = "string"        # Optional: Source session ID
generation_timestamp = "datetime" # Optional: When generated
manually_edited = false          # Optional: Has been manually modified

[usage]
context = "string"               # Optional: Usage context
framework = "string"             # Optional: Framework/technology
language = "string"              # Optional: Programming language

[tags]
# Includes the common [tags] section.
```

---

### Output Style Schema

A system prompt modification for Claude Code.

```toml
[output_style]
# Includes all Core Attributes.
name = "string"                  # Required: Style name (matches id)

[author]
# Includes the common [author] section.

[usage]
scope = "string"                 # Optional: "project" or "user"
activation = "string"            # Optional: How to activate (e.g., "/output-style explanatory")

[behavior]
maintains_core_capabilities = true  # Optional: Whether core Claude Code features remain
modifies_system_prompt = true       # Optional: Whether this modifies system prompt
focus = "string"                    # Optional: Primary focus area
model = "string"                    # Optional: "opus", "sonnet", "haiku"
insights = false                    # Optional: Whether style provides educational insights
task_completion = true              # Optional: Whether style completes tasks
collaborative = false               # Optional: Whether style requests user input

[source]
type = "string"                  # Optional: "built-in", "external", "adapted", "original"
origin = "string"                # Optional: Source organization/author
url = "string"                   # Optional: Source URL if external
original_author = "string"       # Optional: Original author if external/adapted
license = "string"               # Optional: License information

[changelog]
# Includes the common [changelog] section.

[tags]
# Includes the common [tags] section.
contexts = ["string"]            # Optional: Usage contexts

[lineage]
# Includes the common [lineage] section.
```

---

### Slash Command Schema

An interactive command for Claude Code.

```toml
[command]
# Includes all Core Attributes.
name = "string"                  # Required: Command name (without /)

[author]
# Includes the common [author] section.

[usage]
namespace = "string"             # Optional: Command namespace (e.g., "frontend")
arguments = ["string"]           # Optional: Expected argument names
argument_hint = "string"         # Optional: Hint text for arguments (shown in Claude Code)
file_patterns = ["string"]       # Optional: File glob patterns for context
requires_selection = false       # Optional: Requires text selection
scope = "string"                 # Optional: "project" or "user" (for Claude Code deployment)

[behavior]
allowed_tools = ["string"]       # Optional: Claude Code allowed-tools format
model = "string"                 # Optional: "opus", "sonnet", "haiku"
extended_thinking = false        # Optional: Enable extended thinking mode

# Use either [provenance] OR [source], not both
[provenance]
source_type = "string"           # Optional: "meta-prompt" if generated
source_id = "string"             # Optional: Source meta-prompt ID
source_version = "string"        # Optional: Source version
source_session = "string"        # Optional: Source session ID
generation_timestamp = "datetime" # Optional: When generated
manually_edited = false          # Optional: Has been manually modified

[source]
type = "string"                  # Optional: "external", "adapted", "original"
url = "string"                   # Optional: Source URL if external
original_author = "string"       # Optional: Original author if external/adapted
license = "string"               # Optional: License information
adapted = false                  # Optional: Whether adapted from external source
adaptation_notes = "string"      # Optional: Notes about adaptations made

[changelog]
# Includes the common [changelog] section.

[tags]
# Includes the common [tags] section.
contexts = ["string"]            # Optional: Usage contexts (coding, review, debug)

[lineage]
# Includes the common [lineage] section.
```

---

### Agents.md Schema

Instructions for an AI coding agent.

```toml
[agents-md]
# Includes all Core Attributes.

[author]
# Includes the common [author] section.

[project]
name = "string"                  # Optional: Project name
repository = "string"            # Optional: Project repository URL

[conventions]
coding_style = "string"          # Optional: Link to coding style guide
commit_messages = "string"       # Optional: Commit message conventions
branching_strategy = "string"    # Optional: Branching strategy

[build]
command = "string"               # Optional: Build command
dependencies = ["string"]        # Optional: Build dependencies

[test]
command = "string"               # Optional: Test command
framework = "string"             # Optional: Testing framework

[changelog]
# Includes the common [changelog] section.

[tags]
# Includes the common [tags] section.

[lineage]
# Includes the common [lineage] section.
```

---

### Sub-Agent Schema

A specialized AI assistant for task delegation.

```toml
[sub_agent]
# Includes all Core Attributes.
name = "string"                  # Required: Agent name

[author]
# Includes the common [author] section.

[behavior]
context_isolation = true         # Optional: Whether the agent has isolated context
tool_restrictions = ["string"]   # Optional: List of restricted tools
domain_expertise = ["string"]    # Optional: List of expertise domains

[changelog]
# Includes the common [changelog] section.

[tags]
# Includes the common [tags] section.

[lineage]
# Includes the common [lineage] section.
```



## Validation Rules

### Required Fields
- All `[prompt]`, `[spec]`, or `[command]` sections must have: id, type, title, version, created
- All prompts/commands must have at least one category tag
- Meta-prompts must specify target_types
- External sources should include `[source]` section with type and attribution

### Format Validation
- Versions must follow semantic versioning (v1.0.0)
- Timestamps must be valid ISO8601 format
- IDs must be unique within type
- Email addresses must be valid format (if provided)

### Cross-Reference Validation
- Source references must exist (if specified)
- Parent versions must exist (if specified)
- Generated prompts must reference valid source sessions
