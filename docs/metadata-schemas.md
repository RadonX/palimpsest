# Metadata Schemas

## metadata.toml Schemas

### Meta-Prompt Schema

```toml
[prompt]
id = "string"                    # Required: Unique identifier
type = "meta-prompt"             # Required: Always "meta-prompt"
title = "string"                 # Required: Human-readable title
description = "string"           # Required: Purpose description
version = "string"               # Required: Semantic version (v1.0.0)
created = "datetime"             # Required: ISO8601 timestamp
updated = "datetime"             # Required: Last modification time

[author]
name = "string"                  # Required: Author name
email = "string"                 # Optional: Author email
organization = "string"          # Optional: Organization/team

[generation]
target_types = ["string"]        # Required: What this meta-prompt generates
expected_outputs = ["string"]    # Optional: Expected output categories

[tags]
categories = ["string"]          # Required: At least one category
domains = ["string"]             # Optional: Domain/subject areas
difficulty = "string"            # Optional: beginner|intermediate|advanced

[performance]
usage_count = 0                  # Optional: Number of times used
success_rate = 0.0               # Optional: Success rate (0.0-1.0)
avg_generation_time = 0.0        # Optional: Average time in seconds

[lineage]
parent_version = "string"        # Optional: Previous version
deprecated = false               # Optional: Default false
```

### Regular Prompt Schema

```toml
[prompt]
id = "string"                    # Required: Unique identifier
type = "regular-prompt"          # Required: Always "regular-prompt"
title = "string"                 # Required: Human-readable title
description = "string"           # Required: Purpose description
version = "string"               # Required: Semantic version
created = "datetime"             # Required: Creation timestamp
updated = "datetime"             # Required: Last update timestamp

[author]
name = "string"                  # Required: Author name
email = "string"                 # Optional: Author email

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
categories = ["string"]          # Required: Classification tags
domains = ["string"]             # Optional: Subject domains
```

### Dev Spec Schema

```toml
[spec]
id = "string"                    # Required: Unique identifier
type = "dev-spec"                # Required: Always "dev-spec"
title = "string"                 # Required: Specification title
description = "string"           # Required: What this spec covers
version = "string"               # Required: Semantic version
created = "datetime"             # Required: Creation timestamp

[project]
name = "string"                  # Optional: Project name
component = "string"             # Optional: Component/module name
priority = "string"              # Optional: low|medium|high|critical
estimated_hours = 0              # Optional: Development estimate

[requirements]
functional = ["string"]          # Optional: Functional requirements
non_functional = ["string"]      # Optional: Non-functional requirements

[dependencies]
services = ["string"]            # Optional: Required services
libraries = ["string"]           # Optional: Required libraries

[tags]
categories = ["string"]          # Required: Specification categories
domains = ["string"]             # Optional: Technical domains
```

### Slash Command Schema

```toml
[command]
id = "string"                    # Required: Unique command identifier
type = "slash-command"           # Required: Always "slash-command"
title = "string"                 # Required: Human-readable title
version = "string"               # Required: Semantic version
created = "datetime"             # Required: Creation timestamp
updated = "datetime"             # Required: Last update timestamp

[author]
name = "string"                  # Required: Author name (who added to palimpsest)
email = "string"                 # Optional: Author email

[usage]
arguments = ["string"]           # Optional: Expected argument names
requires_selection = false       # Optional: Requires text selection

[behavior]
tools_allowed = ["string"]       # Optional: Allowed tools (read, write, bash, etc.)
extended_thinking = false        # Optional: Enable extended thinking mode
bash_execution = false           # Optional: Allow bash command execution

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
original_author = "string"       # Optional: Original author if external
license = "string"               # Optional: License information
adapted = false                  # Optional: Whether adapted from external source
adaptation_notes = "string"      # Optional: Notes about adaptations made

[tags]
categories = ["string"]          # Required: Command categories
domains = ["string"]             # Optional: Subject domains
contexts = ["string"]            # Optional: Usage contexts (coding, review, debug)

[lineage]
parent_version = "string"        # Optional: Previous version
deprecated = false               # Optional: Whether deprecated
```

## palimpsest.toml Schema

```toml
[general]
name = "string"                  # Required: Repository name
version = "string"               # Required: Config version
description = "string"           # Optional: Repository description
default_author = "string"        # Optional: Default author name
default_email = "string"         # Optional: Default author email

[versioning]
scheme = "semantic"              # Required: semantic|incremental|timestamp
auto_increment = "patch"         # Optional: major|minor|patch
require_changelog = true         # Optional: Default false

[generation]
auto_track_generated = true      # Optional: Auto-track generated prompts
copy_to_type_directory = true    # Optional: Copy to target directories
preserve_session_artifacts = true # Optional: Keep generation artifacts

[storage]
compression = false              # Optional: Compress files
backup_enabled = true            # Optional: Enable backups
backup_frequency = "daily"       # Optional: daily|weekly|monthly
max_backups = 30                 # Optional: Max backup count

[indexing]
auto_rebuild = true              # Optional: Auto-rebuild indices
rebuild_frequency = "on_change"  # Optional: on_change|hourly|daily
include_content_search = true    # Optional: Index file contents

[templates]
default_meta_prompt = "string"   # Optional: Default template file
default_regular_prompt = "string" # Optional: Default template file
default_dev_spec = "string"      # Optional: Default template file
default_slash_command = "string" # Optional: Default template file

[validation]
require_metadata = true          # Optional: Require metadata.toml
require_tags = ["string"]        # Optional: Required tag categories
validate_provenance = true       # Optional: Validate source links
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