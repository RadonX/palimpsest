# Palimpsest Documentation

Palimpsest is a filesystem‑first system for managing prompts, output styles, and project commands for Claude Code. Assets are plain files, versioned semantically, and tracked with explicit metadata and provenance.

## Start Here
- `directory-structure.md`: Repository layout and where things live.
- `usage-guide.md`: How to install and use assets in Claude Code.
- `asset-versioning-guide.md`: Create a new version and update `latest.md`.

## Docs Map
- Core Reference
  - `project-agreement.md`: Goals, scope, and key decisions.
  - `directory-structure.md`: Canonical layout and naming.
  - `file-formats.md`: TOML/Markdown/JSON/JSONL conventions.
  - `metadata-schemas.md`: Canonical metadata tables (single source of truth).
  - `provenance-tracking.md`: Lineage, sessions, and audit trail.
- Asset Guides
  - `output-style-guide.md`: What output styles are and how to structure them.
  - `slash-command-best-practices.md`: Frontmatter, tools, naming, and safety.
  - `slash-command-workflow.md`: Creating links, sessions, and updates.
- How‑To
  - `asset-versioning-guide.md`: Add a new version and edit `metadata.toml`.
  - `usage-guide.md`: Copy assets into user/project paths and run.

## Maintenance & Conventions
- Single source of truth: schemas live in `metadata-schemas.md`. Do not redefine `[source]`, `[provenance]`, or field types elsewhere.
- Versioning: never edit old `versions/vX.Y.Z`; add a new version and relink `latest.md`. Sessions use `session-YYYYMMDD-HHMMSS-vX.Y.Z.jsonl`.
- Naming: IDs are kebab‑case; filenames are fixed per type (`command.md`, `system_prompt.md`, `agents.md`); versions use `vMAJOR.MINOR.PATCH`.
- Attribution & generators: record origins via `[source]` (see schema). If AI‑generated, include `[source].generator_model` (use `claude-sonnet-4` in examples). Runtime model stays in `[behavior].model`.
- Keep docs DRY: link to the schema for field details; use minimal examples in guides.
- Consistency checks: verify `latest.md` symlinks resolve; grep docs for stale model or command examples when updating.

Keep this file as the entry point; when adding/changing docs, update links and summaries here.
