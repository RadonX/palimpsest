# Usage Guide

This repository contains prompts and commands for Claude Code. Here's how to use them.

## Using Slash Commands

### Installation
Copy the command content from `prompts/slash-commands/{command-name}/latest.md` to your Claude Code commands directory:

```bash
# Copy to user-level commands
cp prompts/slash-commands/think/latest.md ~/.claude/commands/think.md

# Copy to project-level commands  
cp prompts/slash-commands/linus/latest.md .claude/commands/linus.md
```

### Usage in Claude Code
```bash
# Use the command
/think "How should I approach this complex refactoring?"
/linus "Review this code for performance issues"
```

## Using Output Styles

### Installation
Copy the system prompt from `prompts/output-style/{style-name}/latest.md`:

```bash
# Copy to user-level styles
cp prompts/output-style/explanatory/latest.md ~/.claude/output-styles/explanatory.md

# Copy to project-level styles
cp prompts/output-style/learning/latest.md .claude/output-styles/learning.md
```

### Activation in Claude Code
```bash
# Switch to a style
/output-style explanatory
/output-style learning
```

## Browsing Assets

### By Category
- **Analysis & Thinking**: `/think`, `/think-hard`, `/think-harder`, `/think-ultra`
- **Code Review**: `/linus` (Torvalds-style code review)
- **Educational**: `explanatory` and `learning` output styles

### Metadata Information
Each asset includes metadata with:
- **Description**: What the asset does
- **Usage**: How to use it effectively  
- **Tags**: Categories and contexts
- **Author**: Who created it
- **Version**: Current version and changelog

Check `metadata.toml` files for detailed information about each asset.