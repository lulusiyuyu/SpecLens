---
status: draft
maps_to: "templates/"
lang: en
---

# Templates — Index

## Overview

The `templates/` directory contains standard Markdown templates for every type of Spec file that SpecLens generates. Skills reference these templates to ensure consistent formatting across all generated Specs. Templates use placeholder syntax (`{{...}}`) for values that should be filled in by the Agent.

## Modules

| Module | Source Path | One-line Description |
|--------|-----------|---------------------|
| spec_file.md | `templates/spec_file.md` | Standard template for individual module Spec files |
| _index.md | `templates/_index.md` | Template for directory-level navigation/index files |
| overview.md | `templates/overview.md` | Template for the top-level project overview |
| architecture.md | `templates/architecture.md` | Template for architecture decisions document |
| data_flow.md | `templates/data_flow.md` | Template for data flow documentation |
| _mapping.md | `templates/_mapping.md` | Template for Spec ↔ Source mapping table |
| _glossary.md | `templates/_glossary.md` | Template for project glossary/terminology |

## Module Relationships

- All templates are consumed by Skills (especially Analyze and Expand)
- Templates define the output format contract — changing a template affects all future Spec generation
- Templates are independent of each other (no cross-references)

## Notes

Templates use YAML frontmatter for metadata and Markdown for content structure. The `{{placeholder}}` syntax indicates values that should be replaced by the Agent during Spec generation.
