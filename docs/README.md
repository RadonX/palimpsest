# Palimpsest Documentation

This directory contains the project documentation for the Palimpsest prompt management system.

## Documents

- **[project-agreement.md](project-agreement.md)** - Core project specifications and agreements
- **[directory-structure.md](directory-structure.md)** - Complete directory layout and organization
- **[asset-versioning-guide.md](asset-versioning-guide.md)** - Guide for versioning assets
- **[file-formats.md](file-formats.md)** - Detailed file format specifications
- **[metadata-schemas.md](metadata-schemas.md)** - TOML and JSON schema definitions
- **[usage-guide.md](usage-guide.md)** - How to use the system
- **[provenance-tracking.md](provenance-tracking.md)** - How generation tracking works
- **[slash-command-best-practices.md](slash-command-best-practices.md)** - Best practices for Claude Code slash commands
- **[slash-command-workflow.md](slash-command-workflow.md)** - Complete workflow for adding slash commands with symbolic links

## Quick Reference

Palimpsest is a filesystem-based layout for storing:
- Meta prompts (that generate other prompts)
- Regular prompts  
- Development specifications
- All conversations that authored each version
- Generated sessions from each prompt version
- Complete provenance tracking from meta-prompts to generated prompts