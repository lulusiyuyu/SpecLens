---
status: draft
lang: en
---

# SpecLens — Spec ↔ Source Mapping

> This file maps each Spec file to its corresponding source file(s) in the SpecLens project.

## Mapping Table

| Spec File | Source File(s) | Status | Notes |
|-----------|---------------|--------|-------|
| `00_overview.md` | (project-wide) | draft | Project overview |
| `01_architecture.md` | (project-wide) | draft | Architecture decisions |
| `02_data_flow.md` | (project-wide) | draft | Data flow paths |
| `skills/_index.md` | `skills/` | draft | Skills directory index |
| `skills/analyze.md` | `skills/analyze/SKILL.md` | skeleton | Analyze Skill spec |
| `skills/expand.md` | `skills/expand/SKILL.md` | skeleton | Expand Skill spec |
| `templates/_index.md` | `templates/` | draft | Templates directory index |
| `templates/spec_file.md` | `templates/spec_file.md` | skeleton | Spec file template spec |
| `templates/overview.md` | `templates/overview.md` | skeleton | Overview template spec |
| `templates/architecture.md` | `templates/architecture.md` | skeleton | Architecture template spec |
| `templates/data_flow.md` | `templates/data_flow.md` | skeleton | Data flow template spec |
| `templates/_index_template.md` | `templates/_index.md` | skeleton | Index template spec |
| `templates/_mapping_template.md` | `templates/_mapping.md` | skeleton | Mapping template spec |
| `templates/_glossary_template.md` | `templates/_glossary.md` | skeleton | Glossary template spec |

## Unmapped Source Files

| Source File | Reason |
|------------|--------|
| `.gitignore` | Configuration file, not relevant for Specs |
| `README.md` | Project documentation, covered by `00_overview.md` |
| `SpecsDriven_project_context.md` | Project context document, covered by overview + architecture |
| `TODOLIST.md` | Task tracking, not a code module |
