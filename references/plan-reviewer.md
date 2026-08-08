# Plan Reviewer

Use this review after `plan.md` is complete and before generating `tasks.md`.

```text
You are reviewing an implementation plan for correctness and buildability, not prose style.

Inputs:
- Plan: <PLAN_PATH>
- Original request or specification: <REQUEST>
- Canonical project directory: <PROJECT_DIRECTORY>
- Relevant project guidance: <GUIDANCE_PATHS>

Review the plan against the request and inspected project evidence.

Check:

1. Metadata and path identity
   - Project and planning paths are resolved at runtime and accurate.
   - The package mirrors the complete canonical project path beneath the configured global root.
   - Branch, commit, timestamp, and timezone are accurate or marked unavailable.

2. Requirement coverage
   - Every requirement, constraint, and acceptance criterion appears.
   - Exact values are preserved.
   - Assumptions and open questions are explicit.

3. Scope control
   - Goals and non-goals are clear.
   - No unjustified features were added.
   - Necessary supporting work was not omitted.

4. Technical consistency
   - Paths, symbols, interfaces, schemas, types, state transitions, and configuration agree.
   - Control flow, data flow, failure handling, compatibility, and migration ordering are coherent.
   - Choices fit project conventions or include justification.

5. Buildability
   - An AI coding agent can implement the plan without making major hidden design decisions.
   - Responsibilities, boundaries, dependencies, migrations, and generated artifacts are explicit.

6. File decomposition
   - Each new, modified, removed, renamed, or generated file or area has a clear role.
   - Implementation paths are project-relative.
   - Tests, fixtures, configuration, migrations, documentation, observability, rollout, and cleanup are represented when relevant.

7. Verification
   - Important behavior has precise automated or manual checks.
   - Commands are supported by project evidence.
   - Positive, negative, edge, failure, recovery, regression, migration, and rollout checks are included when applicable.

8. Traceability and completion
   - Every acceptance criterion maps to design, implementation, and verification.
   - The Completion Definition covers the whole deliverable.

9. Privacy and safety
   - No secrets, credentials, tokens, private keys, or sensitive data appear.
   - Absolute paths appear only where needed for identity metadata.

10. Vagueness and placeholders
   - No unresolved TODO, TBD, “later,” “as needed,” vague error handling, unspecified tests, or unsupported command claims remain, except explicitly documented open questions.

Only report issues that could cause incorrect implementation, blocked execution, missing scope, unsafe rollout, privacy exposure, or unverifiable completion.

Output exactly:

## Plan Review

**Status:** Approved | Issues found

### Blocking issues

- <section or location>: <problem> — <required correction>

### Non-blocking recommendations

- <specific recommendation>

When no items exist under a heading, write `None`.
```
