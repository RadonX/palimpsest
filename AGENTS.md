# Repository Guidelines

## Start Here
- Layout: `docs/directory-structure.md`
- Use in Claude Code: `docs/usage-guide.md`
- Versioning workflow: `docs/asset-versioning-guide.md`

## Project Layout
- `docs/`: Reference and guides (schemas, versioning, usage).
- `prompts/`:
  - `slash-commands/{id}/versions/vX.Y.Z/{command.md,metadata.toml}`, `latest.md`, optional `sessions/`.
  - `output-style/{id}/versions/vX.Y.Z/system_prompt.md` + `metadata.toml`, `latest.md`.
  - `agents-md/{id}/versions/vX.Y.Z/agents.md` + `metadata.toml`, `latest.md`.
- `templates/`: Starters (e.g., `templates/slash-command-template.md`).

## Common Tasks
- New version (slash command example):
  - `mkdir -p prompts/slash-commands/<id>/versions/v1.1.0`
  - `cp prompts/slash-commands/<id>/versions/v1.0.0/{command.md,metadata.toml} prompts/slash-commands/<id>/versions/v1.1.0/`
  - `cd prompts/slash-commands/<id> && rm -f latest.md && ln -sf versions/v1.1.0/command.md latest.md`
- Quick checks:
  - `test -L latest.md && test -e "$(readlink latest.md)"`
  - `grep -F 'version = "v1.1.0"' versions/v1.1.0/metadata.toml`

## Conventions
- IDs: kebab-case; versions: `vMAJOR.MINOR.PATCH`; never modify old versions.
- Metadata tables per type: `[command]`, `[output_style]`, `[agents-md]` (see `docs/metadata-schemas.md`).
- Origins: record in `[source]`. If AI‑generated, add `[source].generator_model` (e.g., "claude-sonnet-4"). Runtime model lives in `[behavior].model`.
- No secrets; keep `allowed_tools` minimal.

## Testing & PRs
- Sessions: `session-YYYYMMDD-HHMMSS-vX.Y.Z.jsonl`.
- PR checklist: explain changes; link issues; update `metadata.toml` (version/dates/changelog) and `latest.md`; include a usage snippet; do not edit prior versions.

## Docs
- Canonical schemas and maintenance: see `docs/README.md` (Docs Maintenance) and `docs/metadata-schemas.md`.
