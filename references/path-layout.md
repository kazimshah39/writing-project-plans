# Path Layout Reference

Use this reference when mapping the canonical project path into the global plans root.

## Conceptual layout

```text
<global-plans-root>/<mirrored-canonical-project-path>/
└── YYYY-MM-DD-HHmmss-<plan-slug>/
    ├── plan.md
    └── tasks.md
```

All placeholder values are resolved at runtime.

## POSIX paths

For a canonical project path with the form:

```text
/<project-path-components>
```

remove only the leading filesystem separator and append the remaining components beneath the global plans root:

```text
<global-plans-root>/<project-path-components>
```

Preserve the canonical path components. Do not replace them with a shortened project slug.

## Windows drive paths

For a canonical project path with the form:

```text
<drive-letter>:\<project-path-components>
```

map it to:

```text
<global-plans-root>/<drive-letter>/<project-path-components>
```

Rules:

- Detect the drive letter at runtime.
- Remove the colon.
- Convert separators into the platform-appropriate separator used for creating the target path.
- Never assume a particular drive letter or user directory.

## Windows UNC paths

For a canonical UNC path with the form:

```text
\\<server>\<share>\<project-path-components>
```

map it to:

```text
<global-plans-root>/UNC/<server>/<share>/<project-path-components>
```

## Safety checks

Before creating directories:

- Confirm the project path is absolute and canonicalized.
- Reject unresolved `..` components.
- Confirm the resulting planning root remains beneath the selected global plans root.
- Do not include credentials, tokens, query strings, or other secret values.
- Create missing parent directories safely.
- Do not overwrite an existing planning package.

## Project path metadata

Record these values in `plan.md`:

- Original project directory, when different from the canonical path.
- Canonical project directory.
- Global plans root.
- Project planning root.
- Planning package directory.
- Created timestamp including timezone offset.
- Version-control branch and commit when available.

Absolute paths belong in this metadata only. Implementation sections should use project-relative paths.

## Configurability

Select the global root in this order:

1. User-supplied location.
2. `AGENT_PLANS_ROOT`.
3. `~/.agent/plans`.

This default is a convention, not a machine-specific assumption. Expand it at runtime and allow the user or environment to override it.
