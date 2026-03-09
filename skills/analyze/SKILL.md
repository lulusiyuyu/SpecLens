---
name: Analyze
description: >
  Analyze a codebase and generate a mirrored Specs folder skeleton.
  Produces layered specification documents from macro to micro,
  with top-level files filled in and inner files as skeleton placeholders.
input: Local project path (codebase root directory)
output: A `specs-for-{project}/` folder mirroring the source structure
tags: [reverse-engineering, learning, analysis]
---

# Skill: Analyze

> Analyze a codebase and generate a mirrored Specs folder with layered specification documents.

## When to Use

- You want to understand a new or unfamiliar codebase
- You want to create structured documentation for an existing project
- You want to prepare a project for Specs-Driven development

## Parameters

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `project_path` | Yes | — | Absolute path to the project root directory |
| `output_path` | No | `specs-for-{project-name}/` | Where to write the generated Specs |
| `lang` | No | `en` | Language for generated Specs (`en` or `zh`) |

## Instructions for the Agent

You are about to analyze a codebase and generate a complete Specs folder. Follow these steps precisely.

### Step 1: Reconnaissance — Understand the Project

1. **Read the project root directory** listing (top-level files and folders).
2. **Read the README** (or equivalent: `README.md`, `README.rst`, `readme.txt`). If none exists, note this.
3. **Read key entry files**: look for `main.*`, `index.*`, `app.*`, `server.*`, `cli.*`, `__main__.py`, `cmd/`, `src/main.*` or equivalent entry points.
4. **Read configuration files**: `package.json`, `Cargo.toml`, `pyproject.toml`, `go.mod`, `pom.xml`, `build.gradle`, `Makefile`, `Dockerfile`, `tsconfig.json`, etc.
5. **Identify**:
   - Project name
   - Primary programming language(s)
   - Framework(s) and key libraries
   - Project type (CLI tool, web app, library, API server, etc.)
   - Build system and package manager
   - Testing framework
   - Core source directory (e.g., `src/`, `lib/`, `pkg/`, `internal/`)

### Step 2: Map the Source Structure

1. **Recursively list the source directory** (the primary code directory, not tests/docs/config).
2. **Identify core modules**: directories or files that represent major functional units.
3. **Identify cross-cutting concerns**: patterns like error handling, logging, auth, configuration that span multiple modules.
4. **Create a mental model** of the module dependency graph.

### Step 3: Generate the Specs Folder Structure

Create the output directory and mirror the source structure:

```
{output_path}/
├── 00_overview.md
├── 01_architecture.md
├── 02_data_flow.md
├── _mapping.md
├── _glossary.md
│
├── {source-dir}/            ← mirrors the project's source directory
│   ├── _index.md
│   ├── {subdir-1}/
│   │   ├── _index.md
│   │   └── {file}.md       ← skeleton spec for key source files
│   ├── {subdir-2}/
│   │   ├── _index.md
│   │   └── ...
│   └── ...
│
└── _cross-cutting/          ← only if cross-cutting concerns are identified
    ├── error_handling.md
    ├── logging.md
    └── ...
```

**Rules**:
- Mirror the source code directory structure, NOT the entire project (skip `tests/`, `docs/`, `node_modules/`, `vendor/`, `.git/`, build output, etc.)
- Every directory gets an `_index.md`
- Key source files (not utility/trivial files) get their own `{filename}.md` spec
- Use the templates from `templates/` as the base format for each file type

### Step 4: Write Top-Level Files (with Content)

These files should be **filled in** with real content (not skeleton):

#### `00_overview.md`
Use the template from `templates/overview.md`. Fill in:
- Project description (from README + your analysis)
- Tech stack table (populated with real values)
- Architecture diagram (Mermaid — a high-level component diagram)
- Core modules summary table
- Entry points
- Navigation links to sub-specs

#### `01_architecture.md`
Use the template from `templates/architecture.md`. Fill in:
- Architecture style identification
- High-level architecture diagram (Mermaid)
- Key architecture decisions (inferred from code structure and config)
- Module responsibilities table
- Dependency direction description

#### `02_data_flow.md`
Use the template from `templates/data_flow.md`. Fill in:
- Primary end-to-end data paths (at least 2-3 main flows)
- Data flow diagram (Mermaid)
- Data transformation points
- Persistence layer description
- External integrations

### Step 5: Write `_index.md` for Every Directory

Use the template from `templates/_index.md`. For each directory:
- Write a one-paragraph overview of what this directory is responsible for
- Populate the modules table with each child module/file and a one-line description
- Briefly describe module relationships within the directory

### Step 6: Write Skeleton Specs for Key Source Files

Use the template from `templates/spec_file.md`. For each key source file:
- Set `status: skeleton` in frontmatter
- Set `maps_to:` to the relative source file path
- Fill in **only** the `# Module Name` heading and `## One-line Summary`
- Leave all other sections as template placeholders
- These will be expanded later using the **Expand** skill

**What counts as a "key source file"**:
- Files that define core business logic
- Files that define public APIs or interfaces
- Files that implement major features
- Entry point files
- NOT: test files, generated files, config files, trivial utility files

### Step 7: Write `_mapping.md`

Use the template from `templates/_mapping.md`:
- Populate the mapping table with ALL generated spec files and their corresponding source paths
- List any significant source files that were intentionally not given a spec under "Unmapped Source Files"

### Step 8: Write `_glossary.md`

Use the template from `templates/_glossary.md`:
- Extract domain-specific terms from the README, code comments, and naming conventions
- Define each term clearly
- Include abbreviations commonly used in the codebase

### Step 9: Final Review

Before finishing:
1. Verify the folder structure mirrors the source code structure
2. Verify all `_index.md` files have been created
3. Verify all YAML frontmatter is valid
4. Verify top-level files have real content (not just placeholder)
5. Verify skeleton specs have `status: skeleton`
6. Report a summary: total files generated, modules found, technologies identified

## Output Format

After completion, report:
```
✅ Specs generated at: {output_path}/
   - Top-level files: 5 (overview, architecture, data_flow, mapping, glossary)
   - Directory index files: {N}
   - Skeleton specs: {N}
   - Total files: {N}
   - Tech stack: {languages}, {frameworks}
   - Core modules identified: {list}
```

## Language Handling

If `lang: zh`, use Chinese for all generated content:
- Section headings: `## 一句话描述`, `## 职责`, `## 输入/输出`, `## 关键约束`, `## 与其他模块的关系`, `## 实现笔记`
- Descriptions and prose in Chinese
- Keep technical terms, code references, and file paths in English
- `_glossary.md` should include both Chinese and English for each term

If `lang: en` (default), use English for all content.
