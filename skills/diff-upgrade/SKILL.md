---
name: Diff & Upgrade
description: >
  Compare current Specs against a previous version (via Git diff), identify intent changes,
  generate a human-readable change summary, and produce a code modification task list.
input: A Specs folder under Git version control (with uncommitted or cross-commit changes)
output: A change summary + actionable code modification task list
tags: [maintenance, upgrade, diff, evolution]
---

# Skill: Diff & Upgrade

> Detect Specs changes, interpret the intent behind them, and generate a plan to bring code in sync.

## When to Use

- You modified Specs to reflect a new requirement and want to propagate changes to code
- You want to review what changed between two versions of Specs (before/after comparison)
- You want a human-readable changelog derived from Specs diffs
- You want to drive code modifications from Specs changes (Specs-Driven development)

## Parameters

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `specs_path` | Yes | — | Path to the Specs folder root |
| `project_path` | No | (inferred from `_mapping.md`) | Root of the source project |
| `compare` | No | `HEAD` | What to diff against: `HEAD` (uncommitted changes), a commit hash, a branch name, or a tag |
| `scope` | No | `all` | Which specs to analyze: `all`, or a specific spec file/directory path |
| `execute` | No | `false` | If `true`, execute the code modifications after generating the plan |
| `lang` | No | `en` | Language for the output (`en` or `zh`) |

## Instructions for the Agent

You are about to analyze changes in a Specs folder, interpret the intent behind each change, and generate an actionable modification plan. Follow these steps precisely.

### Step 1: Identify Changed Specs

1. **Navigate to the Specs folder** at `specs_path`.
2. **Run `git diff`** to detect changes:
   - If `compare` is `HEAD`: diff uncommitted changes against the last commit
   - If `compare` is a commit/branch/tag: diff current state against that reference
   - Restrict the diff to `scope` if specified
3. **Categorize changes**:
   - **Added files**: new specs that didn't exist before
   - **Deleted files**: specs that were removed
   - **Modified files**: specs with content changes
4. **Read each changed file** (both old and new versions if modified).

### Step 2: Analyze Intent Changes

For each changed spec, identify what the change means at the intent level:

#### For Modified Specs

Compare old vs. new content section by section:

1. **One-line Summary changed** → The module's core purpose has shifted
2. **Responsibilities added/removed** → Scope of the module has expanded or contracted
3. **Input/Output changed** → Interface contract has changed
4. **Key Constraints added/modified** → New requirements (performance, security, etc.)
5. **Relationships changed** → Module dependencies have shifted
6. **Implementation Notes changed** → Technical approach has been revised

For each section change, determine:
- **What changed**: the literal diff
- **Why it changed**: the inferred intent (requirement change, architecture refactor, bug fix, optimization, etc.)
- **Impact level**: `breaking` (interface change), `major` (behavior change), `minor` (internal change), `cosmetic` (wording only)

#### For Added Specs

- A new module is being introduced
- Check if it overlaps with existing modules
- Identify where it fits in the architecture

#### For Deleted Specs

- A module is being removed or merged
- Check if other specs still reference the deleted spec
- Identify cleanup tasks in code

### Step 3: Generate Human-Readable Change Summary

Produce a clear summary document:

```markdown
# Specs Change Summary

**Specs Path**: {specs_path}
**Compared Against**: {compare}
**Generated At**: {YYYY-MM-DD HH:MM}

## Overview

- **Specs modified**: {N}
- **Specs added**: {N}
- **Specs deleted**: {N}
- **Impact level**: {breaking / major / minor / cosmetic}

## Changes

### 1. {Spec file path}

**Impact**: {breaking / major / minor / cosmetic}
**Intent**: {one-sentence explanation of WHY this changed}

| Section | Change | Detail |
|---------|--------|--------|
| One-line Summary | Modified | Was: "..." → Now: "..." |
| Responsibilities | Added | + "Handle rate limiting for API endpoints" |
| Key Constraints | Modified | Latency requirement changed from 200ms to 50ms |

**Code implications**:
- {What needs to change in the source code}
- {Which files are affected}

### 2. {Next spec file path}

...
```

### Step 4: Generate Code Modification Task List

Translate each intent change into concrete code tasks:

```markdown
# Code Modification Tasks

**Derived from**: Specs diff ({compare} → current)
**Total tasks**: {N}

## Task 1: {Descriptive title}

- **Source Spec**: `{spec_path}`
- **Target files**: `{source_file_1}`, `{source_file_2}`
- **Impact**: {breaking / major / minor}
- **Description**: {What needs to be done in the code}
- **Acceptance criteria** (from Spec constraints):
  - [ ] {criterion 1}
  - [ ] {criterion 2}
- **Dependencies**: {other tasks that must be done first, or "None"}

## Task 2: {Descriptive title}

...

## Execution Order

Recommended order to minimize conflicts:
1. Task {N} — {reason this goes first, e.g., "interface change that others depend on"}
2. Task {M} — ...
3. ...
```

**Rules for task generation**:
- Each task must be self-contained and actionable by an Agent or developer
- Tasks must be ordered by dependency (if Task B depends on Task A's output, A comes first)
- Interface/contract changes come before implementation changes
- Deletion/cleanup tasks come last
- Each task must include acceptance criteria derived from the Spec's Key Constraints

### Step 5: Cross-Reference Validation

Before finalizing:

1. **Check for cascade effects**: If Spec A changed and Spec B depends on A, does B also need updating?
2. **Check for orphaned references**: If a spec was deleted, are there dangling references in other specs?
3. **Check for test implications**: If constraints changed, do test cases need updating?
4. Add cascade and test tasks to the task list if needed.

### Step 6: Execute Code Modifications (Optional)

If `execute: true`:

1. Present the task list to the user for confirmation before starting
2. Execute tasks in the recommended order
3. For each task:
   a. Read the target source file(s)
   b. Make the necessary modifications following the Spec's intent
   c. Verify the change matches the acceptance criteria
   d. Report completion
4. After all tasks are done, suggest running **Validate** to ensure consistency

If `execute: false` (default):
- Just output the change summary and task list
- The user or another Agent can execute the tasks later

## Output Format

After completion, report:
```
✅ Diff & Upgrade analysis complete: {specs_path}
   - Compared: {compare} → current
   - Specs changed: {N added} / {N modified} / {N deleted}
   - Overall impact: {breaking / major / minor / cosmetic}
   - Code tasks generated: {N}
   - Summary saved to: {specs_path}/_change_summary.md
   - Task list saved to: {specs_path}/_upgrade_tasks.md
```

## Language Handling

If `lang: zh`, generate all output in Chinese:
- Section headings: `## 变更概览`, `## 变更详情`, `## 代码修改任务`, `## 执行顺序`
- Descriptions and intent analysis in Chinese
- Keep file paths, code references, Git commands, and technical identifiers in English

If `lang: en` (default), generate all output in English.

## Tips for Quality

- **Focus on intent, not syntax**: A renaming in a Spec is cosmetic; a new constraint is meaningful. Don't give them equal weight.
- **Be conservative with "breaking"**: Only label changes as breaking if they alter a public interface or contract.
- **Link tasks to specs**: Every code task must trace back to a specific Spec change. No orphan tasks.
- **Respect human edits**: Specs changes represent deliberate human decisions. Don't second-guess the intent — translate it faithfully to code tasks.
- **Preserve existing code style**: When generating code modifications, match the existing project's coding conventions.
