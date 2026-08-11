# Path Layout Reference

Use this reference when mapping a canonical project path to one collision-safe flat directory beneath the global plans root.

## Conceptual layout

```text
<global-plans-root>/<canonical-project-path-slug>--<path-hash>/
└── YYYY-MM-DD-HHmmss-<plan-slug>/
    ├── plan.md
    └── tasks.md
```

All placeholder values are resolved at runtime.

## Flat project directory

1. Canonicalize the project path first.
2. Convert every path separator and unsupported filename character to `-`.
3. Collapse repeated `-` characters and trim leading and trailing `-` characters. Preserve letter case for readability.
4. Limit `<canonical-project-path-slug>` to 120 characters before appending the hash. This keeps the directory name safely within filesystem limits; the hash remains the identity.
5. Compute the SHA-256 digest of the complete canonical project path encoded as UTF-8. Use its first 10 lowercase hexadecimal characters as `<path-hash>`.
6. Join the readable slug and hash with exactly `--`.

```text
<global-plans-root>/<canonical-project-path-slug>--<path-hash>/
```

The hash prevents collisions when different paths become the same slug. Do not omit it, truncate the canonical path before hashing, or use the slug as the identifier.

Examples:

```text
/Users/kazim/local-sites/plovercrm
→ <global-plans-root>/Users-kazim-local-sites-plovercrm--<first-10-sha256>/

/a-b/c
→ <global-plans-root>/a-b-c--<first-10-sha256>/

/a/b-c
→ <global-plans-root>/a-b-c--<different-first-10-sha256>/
```

Apply these same rules to POSIX paths, Windows drive paths, and Windows UNC paths after canonicalization. Never assume a particular drive letter, user directory, server, or share.

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
