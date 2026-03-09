# SpecLens — Project Context

> Turn any codebase into human-readable, Agent-consumable layered specification documents, making Specs a first-class citizen of software.
>
> Specs are the next abstraction layer. Agents are the compiler for this layer.

---

## 1. What is SpecLens

SpecLens is a **Skills / Prompt template system** (not traditional software) that exists as Markdown files and can be loaded into any AI Coding Agent.

It helps users accomplish two core things:

1. **Learn & Understand**: Decompose an existing open-source project into layered Specs files — from macro to micro — enabling rapid comprehension
2. **Develop & Maintain**: Use Specs as the top-level unit of project maintenance, driving Agent code modifications through Spec edits

### Core Philosophy

> **Code is implementation; Specs are intent. Code is disposable; ideas are key.**

```
Traditional:  Human → Code → Product
SpecLens:     Human → Specs → Agent → Code → Product
```

Humans shift from "people who write code" to "people who write specifications." Specs are like a new, higher-level "programming language," and Agents are the "compiler."

### A Deeper Perspective

The history of software development is one of ever-rising abstraction layers: `Assembly → C → Python → Specs`. With each leap, humans move further from "how the machine does it" and closer to "what I want."

- **Specs are not just documentation** — they are the project's API. Agents don't need to read source code; they read Specs to understand and modify a project. The Spec format is essentially **defining a protocol**.
- **Specs are not just descriptions** — they are also acceptance criteria. The "Key Constraints" and "Input/Output" sections naturally describe test cases, from which Agents can automatically derive tests.
- **Specs diffs are human-readable changelogs** — PR reviews shift from code diffs to Specs diffs.

Models will keep getting stronger; context windows will keep growing. SpecLens is not compensating for current model limitations — it is **preemptively defining standards** for the inevitable future.

---

## 2. Problems Solved

| Problem | Current State | How SpecLens Solves It |
|---------|--------------|----------------------|
| Learning a large open-source project is painful | Reading source, searching docs, browsing issues — slow | Auto-generate layered Specs, macro to micro, expand on demand |
| AI Agents easily drift from intent | Lack of structured intent descriptions | Specs serve as explicit intent documents guiding the Agent |
| Project documentation decays | Docs and code are separate, updates fall out of sync | Specs are the documentation and the upstream source of code changes |
| Wanting to participate in debugging during the AI transition | Reading code is hard; reading AI-generated code is harder | Specs structure mirrors source structure — humans can quickly locate and understand |

---

## 3. Product Form

### Form: Skills / Prompt Template System

- **NOT** a web app, desktop app, or CLI tool
- **IS** a set of structured Markdown files (Skills + Templates + Examples)
- Can be loaded into any AI Coding Agent (Claude Code, GitHub Copilot, Gemini CLI, Cursor, Windsurf, etc.)
- Zero dependencies, zero installation, Agent-Agnostic, works with any LLM

### Why This Form

1. **Self-consistent**: The project philosophy is "Specs first, code is disposable" — so the project itself should exist as Specs/Skills, not a pile of code
2. **Maximum coverage**: Not tied to any Agent or LLM, works across all platforms
3. **Zero maintenance cost**: Markdown has no dependencies, no runtime — still readable 10 years from now
4. **Low barrier**: Download the folder, feed it to an Agent, done

---

## 4. Core Capabilities (Implemented as Skills)

### Skill 1: Analyze — Project Analysis & Skeleton Generation

**Input**: A codebase (local project or GitHub URL)
**Output**: A Specs folder skeleton mirroring the source project structure

Behavior:
- Analyze the project's directory structure, tech stack, and core modules
- Generate a Specs folder structure mirroring the source project
- Top-level files (overview, architecture, data_flow) filled with macro-level content
- Inner files contain only skeletons (heading + one-line description), **no details** (lazy loading)
- Generate `_mapping.md` (Spec file ↔ source file mapping table)

### Skill 2: Expand — On-Demand Detail Expansion

**Input**: A specific module/file Spec
**Output**: Detailed Spec content for that module

Behavior:
- Based on the user-specified module, return to the source code for deep analysis
- Fill in responsibilities, input/output, state management, key constraints, relationships with other modules
- Update YAML frontmatter: `status: skeleton → draft`

### Skill 3: Diff & Upgrade — Version Diff & Upgrade

**Input**: Modified Specs (or explicit modification intent)
**Output**: Code change plan + execution

Behavior:
- Compare current Specs against a previous version (via Git diff)
- Identify intent changes
- Generate a code modification task list
- (Optional) Guide the Agent to execute code modifications

### Skill 4: Validate — Specs Consistency Check

**Input**: Current Specs folder
**Output**: Consistency report

Behavior:
- Check for logical contradictions between Specs
- Check Specs vs. actual code consistency
- Check for missing modules
- Check dependency correctness

### Skill 5: Code from Spec — Generate Code from Spec

**Input**: One or more Spec files
**Output**: Corresponding code files

Behavior:
- Read intent, constraints, and interface definitions from the Spec
- Generate code implementation conforming to the Spec
- Run tests to verify

---

## 5. Specs Folder Structure Design

### Core Principles

1. **Mirror the source project structure**: Specs folder hierarchy matches source code directories for easy Human-in-the-Loop navigation
2. **Lazy-loading expansion**: Outer layers generate macro content first; inner layers hold skeleton placeholders, expanded on demand
3. **Every directory has `_index.md`**: Serving as a navigation map for that level
4. **Top-level global perspective files**: overview, architecture, data_flow, glossary

### Structure Example

Given a source project:
```
my-project/
├── src/
│   ├── api/
│   │   ├── routes/
│   │   └── middleware/
│   ├── core/
│   │   ├── engine.ts
│   │   └── scheduler.ts
│   ├── models/
│   └── utils/
├── tests/
└── config/
```

Generated Specs:
```
specs-for-my-project/
├── 00_overview.md              # Project panorama: what, why, architecture diagram
├── 01_architecture.md          # Architecture decisions, tech choices rationale
├── 02_data_flow.md             # How data flows through the system
├── _mapping.md                 # Spec file ↔ source code file mapping
├── _glossary.md                # Glossary of terms
│
├── src/                        # ← mirrors source src/
│   ├── api/
│   │   ├── _index.md           # API layer overview
│   │   ├── routes/
│   │   │   └── _index.md       # Route design (skeleton, expand on demand)
│   │   └── middleware/
│   │       └── _index.md       # Middleware chain description
│   ├── core/
│   │   ├── _index.md           # Core module overview
│   │   ├── engine.md           # Engine responsibilities, I/O, state machine
│   │   └── scheduler.md        # Scheduler strategies and constraints
│   ├── models/
│   │   └── _index.md           # Data model overview + ER diagram
│   └── utils/
│       └── _index.md           # Utility function summary
│
└── _cross-cutting/             # ← added cross-cutting concerns
    ├── error_handling.md
    ├── logging.md
    └── auth.md
```

### Standard Format for a Single Spec File

```markdown
---
status: skeleton | draft | reviewed | stable
maps_to: src/core/engine.ts
last_expanded: 2025-03-08
dependencies:
  - src/models/_index.md
  - src/api/_index.md
---

# Module Name

## One-line Summary
(What this module does, why it exists)

## Responsibilities
- ...

## Input / Output
(What it receives, what it produces)

## Key Constraints
(Performance requirements, security considerations, edge cases)

## Relationships
(Who it depends on, who depends on it, communication patterns)

## Implementation Notes
<!-- EXPANDABLE: Agent fills in technical details on demand -->
```

---

## 6. Three Usage Modes

### Mode 1: Learning Mode (Reverse Engineering)

```
Open-source project → [Skill: Analyze] → Specs skeleton → Browse outer layers
                                                         → Interested module → [Skill: Expand] → Deep details
```

Use cases: Learning a new tech stack, quickly onboarding to a new project, code review

### Mode 2: Development Mode (Forward Engineering)

```
Human idea → Write Specs → [Skill: Code from Spec] → Agent generates code
                                                    → [Skill: Validate] → Consistency check
```

Use cases: New project development, AI-first development workflow

### Mode 3: Maintenance Mode (Iterative Evolution)

```
Specs v1 → Human modifies Specs → Specs v2
         → [Skill: Diff & Upgrade] → Identify intent changes
         → Agent modifies code → Test → Deploy
```

Use cases: Iterative upgrades of existing projects, requirement change management

---

## 7. Versioning Strategy

- **Do NOT use** `specs-v001/`, `specs-v002/` folders
- **Use Git** for Specs version management:
  - Commit after each Specs modification
  - Tag important versions (`v0.1.0`, `v0.2.0`)
  - View intent changes via `git diff`
  - Git natively supports merge, revert, blame, history

---

## 8. Specs Classification System

Not all Specs are the same. Five categories are recommended:

| Type | Icon | Description | Example |
|------|------|-------------|---------|
| Architecture Spec | 📐 | System architecture, module responsibilities, data flow | `01_architecture.md` |
| Feature Spec | 🎯 | Feature descriptions, user stories, acceptance criteria | `feature_search.md` |
| Interface Spec | 🔧 | API contracts, module interface definitions | `api/routes/_index.md` |
| Test Spec | 🧪 | Test strategy, edge cases, expected behavior | `_test_strategy.md` |
| Constraint Spec | 📏 | Performance requirements, security requirements, compatibility | `_constraints.md` |

---

## 9. Relationship to Existing Ecosystem

### Tools to Reference / Combine With

| Tool | Purpose | How to Combine |
|------|---------|---------------|
| **GitHub Spec Kit** | Spec-Driven development templates | Borrow its four-phase workflow template design |
| **SpecFact CLI** | Reverse-generate Specs from code (Python) | Borrow its `code2spec` analysis approach |
| **DeepWiki / deepwiki-open** | AI auto-generate project Wiki | Borrow its auto-generated architecture diagrams and hierarchical doc structure |
| **Codefetch / Gitingest** | Codebase → LLM-friendly format | Can serve as a pre-processing step for the Analyze Skill |
| **AGENTS.md** | AI Agent context standard | Borrow its Agent instruction format |

### SpecLens' Unique Value (What Existing Tools Don't Do)

1. **Mirrors the source project structure** — not abstract functional groupings, but 1:1 correspondence with code directories
2. **Lazy-loading expansion** — doesn't generate all details at once; skeletons first, drill down on demand
3. **Three unified modes** — Learning, Development, and Maintenance share one Specs infrastructure
4. **Human-in-the-Loop friendly** — optimized for the transition period where humans participate in debugging
5. **Pure Skills form** — zero dependencies, Agent-Agnostic, works with any LLM
6. **Specs as project API** — Agents consume Specs, not source code, to understand and modify projects
7. **Specs as acceptance criteria** — constraint descriptions can auto-derive tests, closing the intent → implementation → verification loop

---

## 10. Design Principles

1. **Specs are first-class citizens**: Everything starts from Specs; code is merely a Spec's product
2. **Human readability first**: Specs use language that humans easily understand, not piles of technical jargon
3. **Expand on demand**: No information-overloading full-generation; respect the user's attention
4. **Structure is navigation**: The folder structure itself is a map; no extra index system needed
5. **Agent-Agnostic**: Not tied to any AI platform or LLM; any Agent can use it
6. **Version-friendly**: Naturally compatible with Git; supports diff/merge/history
7. **Self-consistent**: The project itself exists as Specs/Skills, practicing its own philosophy

---

## 11. Key Design Notes

- **Spec granularity**: Describe What and Why, not How. Too fine-grained becomes code, losing abstraction value.
- **Unidirectional dependency**: Always from Specs → Code. The Validate Skill ensures consistency.
- **Models will improve**: Current context window limitations and cross-Agent consistency issues will naturally resolve as models advance. SpecLens doesn't need workarounds for these — just focus on defining format standards.

---

## 12. Project Roadmap

See [TODOLIST.md](./TODOLIST.md) for the detailed executable task list.

**Overall Cadence**:
1. Polish Analyze + Expand Skills → run through real projects end-to-end
2. Dogfooding: Use SpecLens to analyze SpecLens itself
3. Analyze target projects (OpenHands, OpenCode, claude-code) to build an example Gallery
4. Complete remaining Skills (Validate, Diff & Upgrade, Code from Spec)
5. Write README + open-source release

---

## 13. Quick Reference

| Attribute | Value |
|-----------|-------|
| **Project Name** | SpecLens |
| **Product Form** | Skills / Prompt template system (Markdown folder) |
| **Core Philosophy** | Specs first, code is a Spec's product; Specs are the next abstraction layer, Agents are the compiler |
| **Core Capabilities** | Analyze → Expand → Validate → Diff/Upgrade → Code from Spec |
| **Target Users** | Developers using AI Agents for development/learning |
| **Tech Dependencies** | None (pure Markdown, Agent-Agnostic) |
| **Version Management** | Git (branches + tags) |
| **Inspiration** | Twitter Specs-Driven development practice sharing |
| **Competitors/References** | GitHub Spec Kit, SpecFact, DeepWiki |
| **Target Example Projects** | OpenHands, OpenCode, claude-code |
