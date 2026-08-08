# Tasks Reviewer

Use this review after `tasks.md` is generated from the reviewed `plan.md`.

```text
You are reviewing an AI-executable task checklist against its source implementation plan.

Inputs:
- Plan: <PLAN_PATH>
- Tasks: <TASKS_PATH>
- Original request or specification: <REQUEST>
- Canonical project directory: <PROJECT_DIRECTORY>

Check:

1. File relationship
   - `plan.md` and `tasks.md` are in the same planning package.
   - `tasks.md` links to `./plan.md`.
   - Project and package metadata agree.

2. Checklist format
   - Every executable task begins with `- [ ]`.
   - Task IDs are unique, sequential, and consistently formatted.
   - Every task includes Plan reference, Depends on, Files, Action, and at least one Verify line.

3. Plan fidelity
   - Tasks introduce no design, dependency, feature, file, migration, or rollout behavior absent from `plan.md`.
   - Each task points to the plan section authorizing it.
   - Task wording does not contradict plan decisions.

4. Coverage
   - Every requirement, acceptance criterion, implementation area, test, fixture, configuration change, migration, generated file, documentation update, security requirement, observability item, rollout step, and cleanup item is covered when applicable.

5. Sequencing
   - No task relies on a contract, file, schema, fixture, or behavior introduced later.
   - Dependencies refer only to earlier valid task IDs.
   - Migration and rollout ordering is safe.

6. Actionability
   - Each task is a coherent, independently reviewable increment.
   - An AI coding agent can complete it without redesigning the solution.
   - Files, areas, symbols, endpoints, schemas, or configuration are named when available.
   - Actions define concrete behavior and relevant negative or edge cases.

7. Verification
   - Every task has a precise command or manual procedure with an observable result.
   - Commands match project tooling or are explicitly unresolved in the plan.
   - No Verify line says only “test it,” “check it,” or “make sure it works.”

8. Task sizing
   - No task combines unrelated responsibilities.
   - Tasks are not fragmented into trivial edits without independent verification value.

9. Final validation
   - The final task depends on all required implementation work.
   - It runs every applicable quality gate.
   - It confirms documentation and generated artifacts are current.
   - It checks every acceptance criterion.

10. Vague wording
   - No task merely says “improve code,” “fix bugs,” “refactor,” “update tests,” “add docs,” or “handle edge cases” without concrete scope and expected results.

Only report issues that would block reliable execution, leave plan work uncovered, create invalid ordering, add unplanned scope, or make completion unverifiable.

Output exactly:

## Tasks Review

**Status:** Approved | Issues found

### Blocking issues

- <task ID or missing area>: <problem> — <required correction>

### Non-blocking recommendations

- <specific recommendation>

When no items exist under a heading, write `None`.
```
