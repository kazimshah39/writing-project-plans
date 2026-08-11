---
name: writing-project-plans
description: Creates comprehensive implementation plans and sequential AI-executable task checklists before code changes. Use for feature requests, bug fixes, refactors, migrations, architecture changes, specifications, or any software work that benefits from a reviewed plan.md and tasks.md. Stores each planning package outside the project under a configurable global plans root in a collision-safe flat project directory.
metadata:
  version: "1.0.0"
  category: "development"
  tags: "planning,task-breakdown,implementation-plan,coding-agent"
---

# Writing Project Plans

Create an implementation-ready planning package before changing project code.

The package contains:

- `plan.md`: the design and implementation source of truth.
- `tasks.md`: a sequential checklist derived only from the reviewed plan.

Store both files outside the project by default. Stop after planning unless the user separately requests implementation.

## Required workflow

Follow these phases in order:

1. Resolve the project and planning paths.
2. Inspect the project evidence relevant to the request.
3. Clarify or record requirements, assumptions, constraints, and open questions.
4. Create the timestamped planning package directory.
5. Write `plan.md` comprehensively.
6. Review and correct `plan.md`.
7. Derive `tasks.md` from the approved plan.
8. Review and correct `tasks.md`.
9. Report the generated paths and stop.

Do not create `tasks.md` before `plan.md` is complete enough to implement. Do not silently begin implementation.

## Read the bundled references

Use these files from the skill directory:

- Read [references/path-layout.md](references/path-layout.md) when resolving or creating paths.
- Read [references/plan-template.md](references/plan-template.md) before writing `plan.md`.
- Read [references/tasks-template.md](references/tasks-template.md) before writing `tasks.md`.
- Use [references/plan-reviewer.md](references/plan-reviewer.md) for the plan review.
- Use [references/tasks-reviewer.md](references/tasks-reviewer.md) for the task review.

Keep references relative to this skill directory. Do not substitute machine-specific paths into the skill itself.

# Phase 1: Resolve paths

## Determine the project root

Use this precedence:

1. A project directory explicitly supplied by the user.
2. The version-control repository root containing the current working directory.
3. The workspace root supplied by the coding environment.
4. The current working directory as a fallback.

When Git is available, `git rev-parse --show-toplevel` is suitable for detecting the repository root.

## Canonicalize the project path

Resolve the project directory into a canonical absolute path. Resolve `~`, relative segments, symbolic links when supported, and platform-specific separators.

Treat the canonical path as the identity of this checkout. Separate checkouts in separate locations intentionally receive separate planning roots.

## Select the global plans root

Use this precedence:

1. A plans root explicitly supplied by the user.
2. The `AGENT_PLANS_ROOT` environment variable.
3. The default `~/.agent/plans`.

Expand the selected root before use. Keep it outside the project unless the user explicitly requests project-local storage.

## Derive the project planning directory

Create one flat, collision-safe directory beneath the global plans root using the rules in [references/path-layout.md](references/path-layout.md).

The resulting project planning root has this conceptual form:

```text
<global-plans-root>/<canonical-project-path-slug>--<path-hash>/
```

Derive the readable slug and hash from the canonical project path at runtime. Never hard-code a username, home directory, drive letter, workspace directory, project name, or project path.

## Create the planning package

Name each package:

```text
YYYY-MM-DD-HHmmss-<plan-slug>
```

Rules:

- Generate the timestamp from the current local time at runtime.
- Use a 24-hour clock and include seconds.
- Derive `<plan-slug>` from the specific requested outcome.
- Use lowercase kebab-case for the slug.
- Prefer a descriptive slug over generic terms such as `changes` or `updates`.
- If the path already exists, append `-2`, `-3`, and so on.
- Never overwrite an unrelated package.

Create exactly:

```text
<planning-package>/
├── plan.md
└── tasks.md
```

Treat `datas.md` as a typo for `tasks.md` unless the user explicitly requires the former filename.

## Protect private information

The readable project-directory slug can expose local directory names. Keep the global plans root private by default.

Do not place secrets, tokens, credentials, private keys, connection strings, sensitive customer data, or URL query strings in paths or planning files.

# Phase 2: Inspect the project

Base the plan on project evidence instead of generic assumptions.

Inspect only what is relevant, including:

- Repository guidance such as `AGENTS.md`, `CLAUDE.md`, `CONTRIBUTING.md`, and relevant README files.
- Source entry points and modules affected by the requested behavior.
- Existing tests, fixtures, schemas, migrations, configuration, generated files, CI, and release workflows.
- Similar implementations that establish project conventions.
- Package-manager scripts and actual commands for tests, linting, formatting, type checking, and builds.
- Current branch and commit when useful for traceability.

Start with likely entry points, then follow imports, calls, schemas, tests, and configuration. Do not scan the entire repository without a planning reason.

## Handle missing information

Preserve the user's exact requirements and acceptance criteria.

- Use repository evidence for technical details.
- Label assumptions explicitly.
- Record material unresolved decisions as open questions.
- Do not invent product behavior, external contracts, test commands, or file paths.
- When a missing decision prevents a safe implementation design, ask for clarification when interaction is possible. Otherwise document the blocking question and its impact.

# Phase 3: Write plan.md

Use [references/plan-template.md](references/plan-template.md) as the required structure. Adapt headings only when the project makes a section genuinely inapplicable; state why rather than silently omitting important areas.

A complete plan must:

- Explain the current state and intended outcome.
- Separate goals from non-goals.
- Preserve requirements, constraints, and acceptance criteria.
- Define the proposed architecture, behavior, interfaces, data flow, and failure handling.
- Identify specific project-relative files or areas to add, modify, remove, or generate.
- Describe implementation ordering and dependencies.
- Define testing and quality gates using commands supported by project evidence.
- Address migrations, compatibility, rollout, backout, observability, security, documentation, and cleanup when relevant.
- Trace each acceptance criterion to implementation and verification.
- Define what complete means.

## File impact rules

For every expected file or area, record:

- Project-relative path or precise area.
- Whether it is new, modified, removed, renamed, or generated.
- Its responsibility in the change.
- Important symbols, interfaces, schemas, or behavior involved.
- Related tests or validation.

Use absolute paths only in the project-context metadata where identity requires them. Use project-relative paths for implementation work.

## Verification rules

Do not guess commands. Prefer commands found in project scripts, documentation, CI, or existing contributor workflows.

For each validation command, state the expected successful result. When a command cannot be established, identify what must be resolved before execution instead of presenting a guess as fact.

# Phase 4: Review plan.md

Review the plan before deriving tasks.

Use a separate review agent when available. Otherwise perform the same review yourself using [references/plan-reviewer.md](references/plan-reviewer.md).

Correct all blocking issues. Re-run the review until the plan is approved or only explicitly documented blocking questions remain.

The review must check:

- Requirement and acceptance-criterion coverage.
- Internal technical consistency.
- Buildability without major hidden design decisions.
- File and test coverage.
- Migration and rollout safety.
- Verification precision.
- Privacy and secret handling.
- Unresolved placeholders or vague statements.

# Phase 5: Write tasks.md

Derive `tasks.md` only from the reviewed `plan.md`. Do not introduce new design decisions, dependencies, files, requirements, or rollout behavior.

Use [references/tasks-template.md](references/tasks-template.md).

Every executable task must begin with an unchecked Markdown checklist item:

```markdown
- [ ] **T01 — Specific task title**
```

Every task must include:

- `Plan reference:` the authorizing plan section.
- `Depends on:` earlier task IDs or `None`.
- `Files:` expected project-relative files or precise areas.
- `Action:` concrete implementation instructions.
- `Verify:` an exact test, lint, typecheck, build, migration check, or observable manual procedure.

## Task quality rules

Each task must be:

- Small enough for an AI coding agent to complete independently.
- Large enough to produce a coherent, reviewable increment.
- Specific about behavior, files, symbols, schemas, or interfaces when known.
- Ordered so prerequisites are completed first.
- Paired with its relevant tests whenever practical.
- Explicit about important negative, failure, and edge cases.
- Verifiable without relying on vague judgment.

Avoid tasks such as “improve code,” “fix bugs,” “update tests,” “add docs,” or “handle edge cases” unless the exact issue, scope, files, expected behavior, and verification are stated.

Include a final task that runs the complete applicable quality gate and checks every acceptance criterion against the implemented result.

# Phase 6: Review tasks.md

Use a separate review agent when available. Otherwise review with [references/tasks-reviewer.md](references/tasks-reviewer.md).

Correct all blocking issues and re-run the review until approved.

The review must confirm:

- Every executable task uses `- [ ]`.
- IDs and dependencies are valid and sequential.
- Every task contains all required fields.
- The task list covers the full plan without adding scope.
- Ordering is technically safe.
- Verification is precise and supported by project evidence.
- The final validation task covers the whole deliverable.

If task review reveals a missing design decision, update `plan.md` first, review the plan again, then regenerate or repair the affected tasks. Keep the two files synchronized.

# Phase 7: Finish

Report:

- The planning package directory.
- The `plan.md` path.
- The `tasks.md` path.
- Any unresolved blocking questions.
- That implementation has not started.

Do not paste the entire files into the response unless the user asks. Do not implement the plan in the same operation unless the user explicitly requested both planning and implementation.
