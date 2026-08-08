# plan.md Template

Use this structure for the generated `plan.md`. Replace placeholders with project evidence. Remove instructional comments from the final file.

```markdown
# <Plan title>

## Planning Package

- **Created:** `<ISO-8601 timestamp with timezone>`
- **Original project directory:** `<absolute path or Same as canonical>`
- **Canonical project directory:** `<canonical absolute path>`
- **Global plans root:** `<resolved absolute path>`
- **Project planning root:** `<resolved absolute path>`
- **Planning package directory:** `<resolved absolute path>`
- **Version-control branch:** `<branch or Unavailable>`
- **Version-control commit:** `<commit or Unavailable>`
- **Status:** `Planned`

## Executive Summary

Describe the requested outcome, why it is needed, the chosen implementation direction, and the expected user or system result.

## Background and Current State

Explain the existing behavior and architecture relevant to this work. Cite project-relative files, symbols, schemas, configuration, and tests that establish the current state.

## Goals

- <Concrete outcome>

## Non-Goals

- <Explicitly excluded work>

## Requirements and Constraints

### Functional Requirements

- **R1:** <Required behavior>

### Technical Constraints

- **C1:** <Compatibility, architecture, dependency, security, performance, or operational constraint>

### Acceptance Criteria

- **AC1:** <Observable completion criterion>

## Assumptions

- **A1:** <Assumption and supporting evidence>

## Open Questions

- **Q1:** <Question, why it matters, owner or resolution path, and whether it blocks implementation>

Write `None` when there are no open questions.

## Proposed Solution

### Design Overview

Describe the solution and why it fits the current project.

### Component Responsibilities

For each component or layer, define its responsibility, inputs, outputs, dependencies, and failure behavior.

### Control and Data Flow

Describe the important sequence of calls, state changes, data transformations, persistence, events, or user interactions.

### Interfaces and Contracts

Specify relevant APIs, function signatures, types, schemas, events, configuration keys, CLI behavior, or UI contracts. Preserve compatibility requirements.

### Error and Edge-Case Handling

Define validation, expected failures, retries, fallbacks, partial failure behavior, recovery, and user-visible errors.

### Security and Privacy

Describe authorization, authentication, input handling, secret handling, sensitive data, auditability, and abuse protections when applicable. Write `Not applicable` with a reason when appropriate.

## File Impact Map

| Path or area | Change | Responsibility | Important details | Validation |
|---|---|---|---|---|
| `<project-relative path>` | Add/Modify/Remove/Rename/Generate | <Purpose> | <Symbols, schemas, behavior> | <Tests or checks> |

Include source, tests, fixtures, migrations, configuration, generated files, documentation, observability, and cleanup when relevant.

## Implementation Sequence

### 1. <Implementation stage>

- Establish: <contracts or foundations>
- Modify: `<project-relative paths or areas>`
- Behavior: <exact intended change>
- Depends on: <earlier stage or None>
- Validate: <targeted checks>

Repeat in dependency order.

## Testing and Quality Strategy

### Automated Tests

- Unit: <scope and cases>
- Integration: <scope and cases>
- End-to-end or system: <scope and cases>
- Regression: <existing behavior protected>

### Quality Commands

| Purpose | Command | Expected result | Evidence source |
|---|---|---|---|
| Tests | `<command>` | <observable success> | <script, CI, or documentation path> |

Do not invent commands. Mark unresolved commands as a blocking execution prerequisite.

### Manual Validation

1. <Exact procedure>
2. <Observable result>

Use manual validation only where automation is unavailable or insufficient.

## Data, Migration, and Compatibility

Describe schema changes, data migration, backfill, serialization, API compatibility, feature flags, generated artifacts, upgrade order, downgrade behavior, and cleanup. Write `Not applicable` with a reason when appropriate.

## Rollout, Observability, and Backout

- Rollout sequence: <steps>
- Feature gating: <flags or controls>
- Metrics and logs: <signals>
- Alerts: <conditions>
- Backout: <safe reversal procedure>
- Post-rollout cleanup: <temporary code or flags to remove>

Write `Not applicable` with a reason when appropriate.

## Documentation Changes

- `<project-relative documentation path or area>`: <required update>

Write `None` only when no documentation change is justified.

## Risks and Mitigations

| Risk | Likelihood/impact | Mitigation | Validation or monitoring |
|---|---|---|---|
| <Risk> | <Assessment> | <Mitigation> | <Check> |

## Acceptance-Criteria Traceability

| Criterion | Design area | Implementation files or areas | Verification |
|---|---|---|---|
| AC1 | <section> | `<paths>` | <test or procedure> |

## Completion Definition

The work is complete when:

- <All required behavior is implemented>
- <All applicable checks pass>
- <Migrations and generated artifacts are current>
- <Documentation is updated>
- <Rollout and observability requirements are satisfied>
- <Every acceptance criterion is verified>
```

## Plan writing checks

Before review, confirm:

- All requirements appear in the plan.
- Technical claims are supported by project evidence or labeled assumptions.
- File paths are project-relative outside metadata.
- The proposed solution does not hide unresolved architecture decisions.
- Testing covers positive, negative, boundary, failure, and regression behavior when relevant.
- Commands have an evidence source.
- Inapplicable sections explain why.
- No secret values are present.
