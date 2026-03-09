---
status: draft
lang: en
---

# SpecLens — Glossary

> Domain-specific terms used in the SpecLens project and their definitions.

## Terms

| Term | Definition | Also Known As |
|------|-----------|---------------|
| Spec | A structured Markdown document describing a module's purpose, interface, constraints, and relationships | Specification |
| Skill | A Markdown file containing detailed instructions for an AI Agent to perform a specific task | Prompt template |
| Skeleton | A Spec file with only the heading and one-line summary filled in; details pending expansion | Stub, placeholder |
| Expand | The process of filling a skeleton Spec with detailed content by analyzing source code | Deep-dive |
| Analyze | The process of reverse-engineering a codebase into a mirrored Specs folder | Reverse engineering |
| Mirroring | The principle that the Specs folder structure mirrors the source code directory structure | Structure mapping |
| Lazy Loading | The strategy of generating skeleton Specs first and expanding details only on demand | On-demand expansion |
| Frontmatter | YAML metadata block at the top of a Markdown file, delimited by `---` | YAML header |
| Maps-to | The `maps_to` frontmatter field linking a Spec to its corresponding source file | Source mapping |
| Dogfooding | Using SpecLens to analyze the SpecLens project itself | Self-analysis |
| Human-in-the-Loop | Design principle ensuring humans can participate in the AI-driven workflow | HITL |
| Specs-Driven Development | Development methodology where Specs are the primary artifact, code is derived | SDD |
| Cross-cutting Concern | A concern (like logging, auth, error handling) that spans multiple modules | Aspect |

## Abbreviations

| Abbreviation | Full Form |
|-------------|-----------|
| SDD | Specs-Driven Development |
| HITL | Human-in-the-Loop |
| YAML | YAML Ain't Markup Language |
