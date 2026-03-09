# SpecLens — TODOLIST

> This file is the complete executable task list for the project. Read alongside `SpecsDriven_project_context_en.md` — together they provide enough guidance for an Agent to complete the entire project.
>
> **Principle: One perfect example beats a hundred features.**

---

## Phase 0: Project Structure Initialization

- [x] **0.1** Create project directory structure
- [x] **0.2** Initialize Git repository, create `.gitignore`
- [x] **0.3** Create initial README.md (concise version, finalized in Phase 4)

---

## Phase 1: Core Templates + Core Skills

> Goal: Get the Analyze and Expand Skills working end-to-end.

### 1A: Design Templates

- [x] **1A.1** Write `templates/spec_file.md` — standard format for a single Spec file
- [x] **1A.2** Write `templates/_index.md` — navigation template for each directory level
- [x] **1A.3** Write top-level templates (overview / architecture / data_flow / _mapping / _glossary)

### 1B: Write Analyze Skill

- [x] **1B.1** Write `skills/analyze/SKILL.md`

### 1C: Write Expand Skill

- [x] **1C.1** Write `skills/expand/SKILL.md`

---

## Phase 2: Dogfooding + Real-World Project Validation

> Goal: Use SpecLens to analyze real projects, validating and iterating Skill quality.

### 2A: Dogfooding

- [x] **2A.1** Analyze the SpecLens project itself → generate `examples/speclens-self/`
- [x] **2A.2** Review generated results, note areas for Skill improvement
- [x] **2A.3** Iterate and refine the Analyze Skill, regenerate until satisfactory

### 2B: Target Project — OpenHands

- [x] **2B.1** Clone OpenHands project locally
- [x] **2B.2** Generate Specs skeleton for `examples/openhands/`
- [x] **2B.3** Expand 3-5 core module Specs in depth
- [x] **2B.4** Review results, iterate Skills

### 2C: Target Project — OpenCode

- [x] **2C.1** Clone OpenCode project locally
- [x] **2C.2** Generate Specs skeleton for `examples/opencode/`
- [x] **2C.3** Expand 3-5 core module Specs in depth
- [x] **2C.4** Review results, iterate Skills

### 2D: Target Project — claude-code

- [x] **2D.1** Clone claude-code project locally
- [x] **2D.2** Generate Specs skeleton for `examples/claude-code/`
- [x] **2D.3** Expand 3-5 core module Specs in depth
- [x] **2D.4** Review results, iterate Skills

---

## Phase 3: Complete Remaining Skills

> Goal: Deliver all 5 Skills, covering Learning, Development, and Maintenance modes.

- [x] **3.1** Write `skills/validate/SKILL.md` — Specs consistency check
- [x] **3.2** Write `skills/diff-upgrade/SKILL.md` — version diff & upgrade
- [x] **3.3** Write `skills/code-from-spec/SKILL.md` — generate code from Spec

---

## Phase 3.5: Bilingual (Chinese/English) Adaptation

> Goal: All Skills, templates, examples, and docs support both Chinese and English for the international community.

### 3.5A: Skill Bilingual Support

- [x] **3.5A.1** Add `lang` parameter support to every Skill
- [x] **3.5A.2** Add explicit language rules in each Skill's instructions

### 3.5B: Template Bilingual Support

- [x] **3.5B.1** Create Chinese template versions under `templates/zh/`
- [x] **3.5B.2** English templates remain at `templates/` root (default)

### 3.5C: English End-to-End Verification

- [x] **3.5C.1** Verify English Specs output quality for OpenHands
- [x] **3.5C.2** Verify English Specs output quality for OpenCode
- [x] **3.5C.3** Verify English Specs output quality for claude-code
- [x] **3.5C.4** Confirm: consistent structure, equivalent information, complete bilingual glossary

### 3.5D: Project Document Bilingual Versions

- [x] **3.5D.1** Write English version `SpecsDriven_project_context_en.md`
- [x] **3.5D.2** Write English version `TODOLIST_en.md`

---

## Phase 4: README + Open-Source Release

> Goal: Write a README that makes people want to use SpecLens immediately. Bilingual. Then publish.

- [ ] **4.1** Write complete `README.md` (English, as the main repo README):
  - One-line introduction
  - Core philosophy (Specs are the next abstraction layer; Agents are the compiler)
  - 30-second Quick Start (3 steps: download → feed to Agent → see results)
  - Link to an example project's Specs (e.g., `examples/openhands/`)
  - Three usage modes (Learn / Build / Maintain)
  - Skill list with brief descriptions
  - Comparison with existing tools
  - Add `[中文](./README_zh.md)` language toggle at the top

- [ ] **4.2** Write `README_zh.md` (Chinese version):
  - Content mirrors the English version
  - Add `[English](./README.md)` language toggle at the top

- [ ] **4.3** Create GitHub repository and push
- [ ] **4.4** Add example Specs links in both READMEs

---

## Completion Criteria

The project is considered complete when all of the following are met:

1. **All 5 Skill files** are written with clear, Agent-executable instructions
2. **Template files** are complete and format-consistent
3. **At least 3 real-project example Specs** exist under `examples/`
4. **Bilingual support**: Skills support `lang` parameter, README has both Chinese & English versions, at least one example project has English Specs
5. **README** is clear enough for anyone to understand the project and start using it within 3 minutes
6. The project itself has been analyzed by SpecLens (Dogfooding complete)
