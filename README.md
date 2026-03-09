[中文](./README_zh.md)

# SpecLens

> Turn any codebase into human-readable, Agent-consumable layered specification documents.

**Specs are the next abstraction layer. Agents are the compiler.**

```
Traditional:  Human → Code → Product
SpecLens:     Human → Specs → Agent → Code → Product
```

SpecLens is a **Skills / Prompt template system** — a set of structured Markdown files you feed to any AI Coding Agent. Zero dependencies. Zero installation. Agent-Agnostic. Works with any LLM.

---

## Quick Start (30 seconds)

**1. Download**
```bash
git clone https://github.com/lulusiyuyu/SpecLens.git
```

**2. Feed to your Agent**

Point your AI Agent (Claude Code, Copilot, Cursor, Windsurf, Gemini CLI, etc.) to the `skills/` folder. Then ask:

> "Use the Analyze skill on my project at `/path/to/my-project`"

**3. Browse the Specs**

The Agent generates a Specs folder mirroring your project structure — from a high-level overview down to individual module specs. Read the top-level files first; drill into modules on demand.

---

## What Does It Do?

| Problem | How SpecLens Solves It |
|---------|----------------------|
| Learning a large codebase is painful | Auto-generates layered Specs: macro → micro, expand on demand |
| AI Agents drift from your intent | Specs serve as explicit intent documents guiding the Agent |
| Documentation decays | Specs are the documentation *and* the upstream source of code changes |
| Hard to debug AI-generated code | Specs mirror the source structure — navigate and understand quickly |

---

## Three Usage Modes

### 🔍 Learn — Reverse Engineering
```
Codebase → [Analyze] → Specs skeleton → browse top-level
                                       → [Expand] → drill into any module
```
*Understand any project in minutes, not days.*

### 🏗️ Build — Forward Engineering
```
Your idea → write Specs → [Code from Spec] → Agent generates code
                                            → [Validate] → consistency check
```
*Write specs, not code. Let the Agent compile.*

### 🔄 Maintain — Iterative Evolution
```
Specs v1 → edit Specs → Specs v2
         → [Diff & Upgrade] → detect intent changes → Agent updates code
```
*Change the spec, not the code. Review spec diffs, not code diffs.*

---

## Skills

| Skill | Description |
|-------|-------------|
| **[Analyze](skills/analyze/SKILL.md)** | Reverse-engineer a codebase into a mirrored Specs folder skeleton |
| **[Expand](skills/expand/SKILL.md)** | Deep-dive a skeleton spec into full detail |
| **[Validate](skills/validate/SKILL.md)** | Check consistency between Specs and between Specs and code |
| **[Diff & Upgrade](skills/diff-upgrade/SKILL.md)** | Detect Specs changes, generate code modification tasks |
| **[Code from Spec](skills/code-from-spec/SKILL.md)** | Generate code + tests from Spec files |

---

## Example Specs (Real Projects)

Browse Specs generated for real open-source projects:

| Project | Language | Description | Specs |
|---------|----------|-------------|-------|
| **OpenHands** | Python | AI agent platform for software engineering | [examples/openhands/](examples/openhands/) |
| **OpenCode** | Go | Terminal-native AI coding agent | [examples/opencode/](examples/opencode/) |
| **claude-code** | TypeScript | Plugin ecosystem for Claude Code | [examples/claude-code/](examples/claude-code/) |
| **SpecLens** | Markdown | This project (dogfooding) | [examples/speclens-self/](examples/speclens-self/) |

Start with any project's [00_overview.md](examples/openhands/00_overview.md) for the big picture, then navigate deeper.

---

## How Specs Are Structured

Specs mirror the source project's directory structure:

```
specs-for-project/
├── 00_overview.md          # What the project does, tech stack, architecture diagram
├── 01_architecture.md      # Architecture decisions and rationale
├── 02_data_flow.md         # How data flows through the system
├── _mapping.md             # Spec ↔ source file mapping table
├── _glossary.md            # Domain terms glossary
│
├── src/                    # ← mirrors the source directory
│   ├── core/
│   │   ├── _index.md       # Module overview + navigation
│   │   ├── engine.md       # Detailed spec for engine.ts
│   │   └── scheduler.md    # Detailed spec for scheduler.ts
│   └── api/
│       └── _index.md
```

Each spec file follows a [standard template](templates/spec_file.md) with YAML frontmatter and sections: One-line Summary, Responsibilities, Input/Output, Key Constraints, Relationships, Implementation Notes.

---

## Bilingual Support

All Skills support a `lang` parameter (`en` | `zh`). Templates are available in both [English](templates/) and [Chinese](templates/zh/). Project documentation has bilingual versions.

---

## Comparison with Existing Tools

| Tool | SpecLens Difference |
|------|-------------------|
| **DeepWiki** | SpecLens mirrors source structure 1:1; lazy-loads details instead of dumping everything |
| **Codefetch / Gitingest** | Those produce flat LLM-friendly dumps; SpecLens produces navigable, layered specs |
| **GitHub Spec Kit** | Spec Kit is a workflow template; SpecLens is a complete Skills system with 5 executable agents |
| **README / docs** | Docs are static and decay; Specs are version-controlled, validated, and drive code changes |

---

## Philosophy

> Code is implementation. Specs are intent. Code is disposable; ideas are key.

The history of software development is one of ever-rising abstraction: `Assembly → C → Python → Specs`. Each leap moves humans further from "how the machine does it" and closer to "what I want."

- **Specs are the project's API** — Agents read Specs, not source code, to understand and modify projects
- **Specs are acceptance criteria** — Key Constraints naturally describe test cases; Agents derive tests automatically
- **Specs diffs are human-readable changelogs** — Review spec diffs instead of code diffs

Read the full philosophy: [Project Context](SpecsDriven_project_context_en.md)

---

## Project Structure

```
SpecLens/
├── skills/                 # 5 Skills (Agent-executable instructions)
│   ├── analyze/
│   ├── expand/
│   ├── validate/
│   ├── diff-upgrade/
│   └── code-from-spec/
├── templates/              # Spec file templates (en + zh)
│   ├── spec_file.md
│   ├── _index.md
│   ├── overview.md
│   ├── architecture.md
│   ├── data_flow.md
│   ├── _mapping.md
│   ├── _glossary.md
│   └── zh/                 # Chinese templates
├── examples/               # Real-world example Specs
│   ├── openhands/
│   ├── opencode/
│   ├── claude-code/
│   └── speclens-self/
├── SpecsDriven_project_context.md    # Full project context (中文)
├── SpecsDriven_project_context_en.md # Full project context (English)
└── README.md
```

---

## License

MIT
