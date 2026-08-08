# tasks.md Template

Create `tasks.md` only after `plan.md` has passed review.

## Required header

```markdown
# Tasks: <Plan title>

- **Source plan:** [`plan.md`](./plan.md)
- **Project:** `<project name derived at runtime>`
- **Canonical project directory:** `<canonical absolute path>`
- **Planning package:** `<planning package absolute path>`
- **Status:** `Not started`

## Execution Rules

- Complete tasks in dependency order.
- Keep `plan.md` and `tasks.md` synchronized when implementation discoveries require a design change.
- Do not mark a task complete until every `Verify:` check passes.
- Record blockers rather than silently changing scope.
```

## Required task format

Every executable task must use this form:

```markdown
- [ ] **T01 — <Specific task title>**
  - **Plan reference:** `plan.md` — `<authorizing section>`
  - **Depends on:** `None` or `<earlier task IDs>`
  - **Files:** `<project-relative paths or precise areas>`
  - **Action:** <Concrete implementation instructions, expected behavior, and relevant edge or failure cases.>
  - **Verify:** `<command or exact manual procedure>` — <observable expected result>
```

Multiple verification lines are allowed:

```markdown
  - **Verify:** `<targeted test command>` — <expected result>
  - **Verify:** `<lint or typecheck command>` — <expected result>
```

## Decomposition rules

Create tasks in a dependency-safe order. A typical sequence is:

1. Contracts, types, schemas, or test fixtures.
2. Core domain or data behavior.
3. Integration, API, UI, CLI, or workflow wiring.
4. Migration, compatibility, generated artifacts, and configuration.
5. Observability, documentation, rollout, and cleanup.
6. Whole-project validation and acceptance-criteria confirmation.

Adapt the sequence to project evidence.

Each task should:

- Produce one coherent, reviewable increment.
- Name expected files, directories, symbols, endpoints, schemas, or configuration keys when known.
- Include tests with the behavior they verify when practical.
- Define negative and edge behavior where it matters.
- Avoid requiring the executing agent to make a new architectural decision.
- Depend only on tasks that appear earlier.
- Have at least one observable verification result.

Split a task when it contains unrelated responsibilities, different rollback boundaries, or independently reviewable behavior. Do not split work into trivial edits that have no meaningful independent verification.

## Verification rules

A `Verify:` line must contain either:

- A command established by project scripts, documentation, CI, or contributor guidance; or
- A precise manual procedure with an observable expected result.

Invalid verification:

```markdown
- **Verify:** Test it.
- **Verify:** Make sure it works.
- **Verify:** Run the relevant checks.
```

Valid verification describes the exact check and expected result.

## Final task

The last task must validate the complete deliverable. Use this pattern:

```markdown
- [ ] **TNN — Run full validation and confirm acceptance criteria**
  - **Plan reference:** `plan.md` — `Testing and Quality Strategy`, `Acceptance-Criteria Traceability`, and `Completion Definition`
  - **Depends on:** `<all preceding terminal task IDs>`
  - **Files:** `<project-wide areas, generated artifacts, and documentation affected by validation>`
  - **Action:** Run every applicable full quality gate, confirm generated artifacts and documentation are current, and check each acceptance criterion against the implemented behavior. Correct failures without expanding scope beyond the plan.
  - **Verify:** `<full test command>` — <expected result>
  - **Verify:** `<lint/typecheck/build command>` — <expected result>
  - **Verify:** `<acceptance procedure>` — <each acceptance criterion passes>
```

Use only the checks applicable to the actual project. Do not insert guessed commands.

## Coverage check

Before review, map every plan item to at least one task:

- Requirements and acceptance criteria.
- Every file or area in the File Impact Map.
- Tests and fixtures.
- Migrations and compatibility.
- Configuration and generated files.
- Documentation.
- Security and privacy work.
- Observability, rollout, backout, and cleanup.
- Final validation.
