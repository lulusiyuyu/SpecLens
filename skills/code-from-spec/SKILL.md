---
name: Code from Spec
description: >
  Generate code implementation from one or more Spec files.
  Reads intent, constraints, and interfaces from Specs, derives test cases
  from constraints, generates code, and runs tests to verify.
input: One or more Spec files (status draft or higher)
output: Generated source code files + test files
tags: [forward-engineering, development, code-generation]
---

# Skill: Code from Spec

> Generate production-quality code from Spec files, with tests derived from constraints.

## When to Use

- You have written Specs (manually or via Analyze + Expand) and want to generate the corresponding code
- You are starting a new module and want to go from Spec → Code
- You want to regenerate code after modifying a Spec
- You are practicing Specs-Driven development (write Spec first, then generate code)

## Parameters

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `spec_paths` | Yes | — | Path(s) to one or more Spec files to implement |
| `project_path` | Yes | — | Root of the target project where code will be generated |
| `test` | No | `true` | Whether to generate and run tests |
| `style_ref` | No | — | Path to an existing source file to use as a coding style reference |
| `lang` | No | `en` | Language for code comments and documentation (`en` or `zh`) |

## Instructions for the Agent

You are about to generate code from Spec files. The Spec is the source of truth—your code must faithfully implement the intent described in it. Follow these steps precisely.

### Step 1: Read and Understand the Spec(s)

For each spec file in `spec_paths`:

1. **Read the entire spec file** carefully.
2. **Extract from YAML frontmatter**:
   - `maps_to` — the target source file path to generate
   - `dependencies` — related specs that affect this module
   - `status` — must be `draft` or higher (do NOT generate code from `skeleton` specs)
3. **Read dependency specs** listed in `dependencies` to understand:
   - What interfaces this module should consume
   - What contracts this module must respect
4. **Read the parent `_index.md`** to understand where this module fits in the system.
5. **Read `00_overview.md`** to understand the project's tech stack, framework, and conventions.

If `status` is `skeleton`, stop and tell the user to run **Expand** first.

### Step 2: Extract Implementation Requirements

From the spec, extract and organize:

#### Intent
- `## One-line Summary` → The module's core purpose
- `## Responsibilities` → Concrete behaviors to implement

#### Interfaces
- `## Input / Output` → Function signatures, parameter types, return types
- `## Relationships` → What to import, what interface to expose

#### Constraints
- `## Key Constraints` → Non-functional requirements (performance, security, validation rules)
- These will be used to derive test cases

#### Technical Guidance
- `## Implementation Notes` → Specific algorithms, patterns, or approaches to follow

### Step 3: Derive Test Cases from Constraints

Before writing code, derive test cases from the Spec. This ensures testability drives the design.

For each item in `## Key Constraints` and `## Responsibilities`, generate a test case:

```markdown
## Derived Test Cases

### From Responsibilities:
1. "Parse incoming HTTP requests and route them to the correct handler"
   → Test: Given a valid GET /users request, should route to UserHandler
   → Test: Given an unknown route, should return 404

2. "Validate request parameters against the schema"
   → Test: Given valid parameters, should pass validation
   → Test: Given missing required parameter, should return 400 with error message

### From Key Constraints:
1. "Response time must be < 100ms for cached queries"
   → Test: Given a cached query, response time should be under 100ms

2. "Must validate all user input before database operations"
   → Test: Given SQL injection attempt in input, should reject with 400
   → Test: Given XSS payload in input, should sanitize before processing
```

**Rules for test derivation**:
- Each responsibility should have at least one happy-path test and one edge-case test
- Each constraint should have a corresponding verification test
- Security constraints must have explicit negative tests (attack scenarios)
- Performance constraints generate benchmark-style tests if the framework supports it

### Step 4: Determine Code Structure

Based on the tech stack (from `00_overview.md`) and spec content:

1. **Determine the file path**: Use `maps_to` from frontmatter as the target path
2. **Determine the language and framework**: From the project's tech stack
3. **Determine imports**: From the `Relationships` section's `depends_on` entries
4. **Determine the public API**: From `Input / Output` section
5. **If `style_ref` is provided**: Read the reference file and match:
   - Naming conventions (camelCase, snake_case, etc.)
   - Import organization style
   - Comment style and density
   - Error handling patterns
   - File organization (constants at top, etc.)

### Step 5: Generate the Code

Write the source code file at the `maps_to` path:

1. **File header**: Brief comment with module purpose (from One-line Summary)
2. **Imports**: All dependencies identified from Relationships
3. **Types / Interfaces**: Define types for Input/Output if the language supports it
4. **Core implementation**:
   - Implement each responsibility as one or more functions/methods
   - Follow the algorithms described in Implementation Notes
   - Respect all Key Constraints
   - Handle errors as described in the spec
5. **Exports**: Expose the public API as described in Input/Output

**Code quality rules**:
- Follow the project's existing coding conventions (or `style_ref`)
- Add comments only where logic is non-obvious
- Use meaningful variable and function names derived from the spec's terminology
- Implement proper error handling for all external interactions
- Do not over-engineer: implement exactly what the spec describes, nothing more

### Step 6: Generate Test Code

Create a test file alongside the source file (following the project's test conventions):

1. **Test file location**: Follow the project's convention:
   - Same directory: `{file}.test.{ext}` or `{file}_test.{ext}`
   - Test directory: `tests/{module}/{file}.test.{ext}`
   - Mirror structure: `__tests__/{file}.test.{ext}`
2. **Implement each derived test case** from Step 3
3. **Test structure**:
   - Group tests by the spec section they verify (Responsibilities, Constraints)
   - Each test should have a clear description referencing the spec requirement
   - Include setup/teardown as needed
4. **Test types**:
   - Unit tests: For individual functions and methods
   - Integration hints: Add TODO comments for tests that need external services

### Step 7: Run Tests and Verify

If `test: true` (default):

1. **Run the test suite** for the generated code
2. **If tests pass**: Report success
3. **If tests fail**:
   a. Analyze the failure
   b. Determine if it's a code bug or a test bug
   c. Fix the issue (prefer fixing code to match spec, not the other way around)
   d. Re-run tests
   e. Repeat up to 3 times before reporting to the user
4. **Report test results** including pass/fail counts and any remaining issues

### Step 8: Update Spec Status

After successful code generation and testing:

1. Update the spec's `status` from `draft` → `reviewed` (code now exists and passes tests)
2. Update `_mapping.md` to reflect the new status
3. If new dependencies were discovered during implementation, add them to the spec's `dependencies`

## Output Format

After completion, report:
```
✅ Code generated from Spec: {spec_path}
   - Source file: {maps_to}
   - Test file: {test_file_path}
   - Tests: {N passed} / {N total}
   - Spec status: draft → reviewed
   - Dependencies: {list or "unchanged"}
```

For multiple specs:
```
✅ Code generation complete
   - Specs processed: {N}
   - Source files generated: {N}
   - Test files generated: {N}
   - Tests: {passed} / {total}
   - All specs updated to: reviewed
```

## Language Handling

If `lang: zh`, use Chinese for:
- Code comments and documentation strings
- Test descriptions
- Keep all code identifiers (variable names, function names) in English

If `lang: en` (default), use English for all comments and documentation.

## Tips for Quality

- **Spec is the source of truth**: If the spec says "must validate input", you must validate input. No shortcuts.
- **Don't invent requirements**: Only implement what the spec describes. If something is ambiguous, note it as a TODO rather than guessing.
- **Tests prove the spec**: Every test should trace back to a spec requirement. If you can't explain which spec requirement a test verifies, the test is unnecessary.
- **Fail fast on bad specs**: If the spec is too vague to generate code (e.g., skeleton status, missing responsibilities), stop and tell the user to run Expand first.
- **Preserve existing code**: If the target file already exists, diff your changes carefully. Don't overwrite unrelated code. Ask the user before replacing an existing file.
- **Security first**: If the spec mentions any security constraint, implement it thoroughly. Never skip validation, sanitization, or auth checks.
