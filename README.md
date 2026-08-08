# Writing Project Plans

An AI-agent skill for turning software requests into implementation-ready planning packages before code changes begin.

It creates two reviewed Markdown files:

- `plan.md` — the technical design, file impact map, risks, verification strategy, and acceptance-criteria traceability.
- `tasks.md` — a dependency-ordered, AI-executable checklist derived only from the approved plan.

Planning packages are stored outside the project by default, so the working tree remains unchanged.

## When to use it

Use this skill for work that benefits from a reviewed plan, including:

- Features and bug fixes
- Refactors and migrations
- Architecture changes
- Specifications and implementation estimates
- Changes involving multiple files, systems, or rollout risks

## Workflow

The skill follows this sequence:

1. Resolve and canonicalize the project directory.
2. Select a global plans root.
3. Inspect relevant project code, guidance, tests, scripts, and configuration.
4. Record requirements, assumptions, constraints, and blocking questions.
5. Create a timestamped planning package.
6. Write and review `plan.md`.
7. Derive and review `tasks.md` from the approved plan.
8. Report the generated paths and stop without implementing changes.

## Output layout

Packages use this layout:

```text
<plans-root>/<canonical-project-path>/
└── YYYY-MM-DD-HHmmss-<plan-slug>/
    ├── plan.md
    └── tasks.md
```

The plans root is selected in this order:

1. A location supplied by the user
2. The `AGENT_PLANS_ROOT` environment variable
3. `~/.agent/plans`

For POSIX paths, the project’s canonical absolute path is mirrored beneath the plans root without its leading `/`. This keeps plans for separate checkouts separate.

## Using the skill

Ask your compatible coding agent to use `writing-project-plans`, then describe the outcome you want. For example:

```text
Use writing-project-plans to plan a migration from session authentication to OAuth.
```

You can also provide a project directory and plans root explicitly:

```text
Use writing-project-plans to plan the API rate-limit feature for /path/to/project.
Store the planning package under /path/to/plans.
```

The agent should ask about decisions that block a safe design, document non-blocking assumptions and open questions, and stop after generating the plan and tasks.

## Planning standards

### `plan.md`

The implementation plan documents:

- Current state and intended outcome
- Goals and non-goals
- Functional requirements, constraints, and acceptance criteria
- Assumptions and open questions
- Design, responsibilities, data flow, interfaces, and error handling
- Security and privacy considerations
- A project-relative file impact map
- Implementation sequence, testing strategy, rollout, and backout considerations
- Acceptance-criteria traceability and completion definition

### `tasks.md`

Each task is an unchecked checklist item with:

- A sequential task ID
- A reference to the authorizing plan section
- Dependencies
- Affected project-relative files or areas
- Concrete implementation action
- Exact verification steps and expected results

The final task runs all applicable quality gates and confirms every acceptance criterion.

## Safety and quality rules

- Do not create tasks until the plan has been reviewed.
- Do not add new design decisions in `tasks.md`.
- Do not guess project commands, file paths, contracts, or requirements.
- Do not overwrite an existing planning package.
- Keep secrets, tokens, credentials, private keys, connection strings, and sensitive data out of paths and planning files.
- Use absolute paths only for planning-package metadata; describe implementation work with project-relative paths.
- Do not begin implementation unless it is separately requested.

## Included references

| File | Purpose |
|---|---|
| `SKILL.md` | Complete skill instructions and workflow |
| `references/path-layout.md` | Canonical project path and plans-root mapping rules |
| `references/plan-template.md` | Required structure for `plan.md` |
| `references/tasks-template.md` | Required structure for `tasks.md` |
| `references/plan-reviewer.md` | Plan review checklist |
| `references/tasks-reviewer.md` | Task-list review checklist |

## License

No license is currently specified.
