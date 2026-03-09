---
status: draft
maps_to: "skills/"
lang: en
---

# Skills — Index

## Overview

The `skills/` directory contains all SpecLens Skills — structured Markdown instructions that tell AI Agents how to perform specific tasks on codebases and Specs. Each Skill is a self-contained `SKILL.md` file in its own subdirectory, following a consistent format with parameters, step-by-step instructions, and output format specifications.

## Modules

| Module | Source Path | One-line Description |
|--------|-----------|---------------------|
| Analyze | `skills/analyze/SKILL.md` | Reverse-engineer a codebase into a mirrored Specs folder skeleton |
| Expand | `skills/expand/SKILL.md` | Deep-dive a skeleton Spec into a fully detailed specification |
| Validate | `skills/validate/SKILL.md` | Check consistency between Specs and source code |
| Diff & Upgrade | `skills/diff-upgrade/SKILL.md` | Detect Specs changes and generate code modification plans |
| Code from Spec | `skills/code-from-spec/SKILL.md` | Generate code implementation from Spec definitions |

## Module Relationships

Skills form a natural pipeline but can also be used independently:

- **Analyze** produces skeleton Specs that **Expand** consumes
- **Validate** can be run after any Skill to check consistency
- **Diff & Upgrade** operates on versioned Specs (Git history)
- **Code from Spec** takes any detailed Spec as input

All Skills reference the shared `templates/` for output formatting.

## Notes

Each Skill follows a consistent structure: YAML frontmatter (name, description, tags), parameters table, step-by-step agent instructions, output format, and language handling notes.
