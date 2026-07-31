# Project skill template

Use this template for generated repository-specific skills.

Remove sections that genuinely do not apply, but preserve the routing,
boundaries, evidence, and validation sections.

```markdown
---
name: <skill-id>
description: >
  <Describe the tasks, concepts, or affected areas that should cause an agent
  to load this skill.>
type: <orientation|application|domain|cross-cutting|workflow|operations|specialist>
scope:
  - <repository-relative path or glob>
related_skills:
  - <related-skill-id>
last_verified:
  commit: <commit>
  date: <YYYY-MM-DD>
confidence: <high|medium|low>
---

# <Skill title>

## When to use this skill

Use this skill when:

- ...

Typical tasks include:

- ...

Do not use this skill for:

- ...

## Responsibilities and boundaries

This area owns:

- ...

This area does not own:

- ...

## Architecture

<Explain the components, boundaries, and meaningful control or data flow.>

### Important components

| Component | Location | Responsibility |
|---|---|---|
| ... | `path` | ... |

### Main flow

1. ...
2. ...
3. ...

## Project terminology

| Term | Meaning in this repository |
|---|---|
| ... | ... |

## Important entry points

- [`path`](relative-link): explanation.
- [`path`](relative-link): explanation.

## Dependencies and consumers

### Depends on

- ...

### Consumed by

- ...

### External systems

- ...

## Invariants

The following must remain true:

1. ...
2. ...
3. ...

## Common change workflows

### <Workflow name>

Use this process when ...

1. ...
2. ...
3. ...

Files commonly changed together:

- `path`
- `path`

Validation:

```bash
<verified commands>
````

## Testing and validation

Run for all changes in this area:

```bash
<verified commands>
```

Run conditionally:

* ...

## Operational considerations

* ...

## Common mistakes

* Do not ...
* Prefer ...
* Be aware that ...

## Legacy and deprecated patterns

* ...

Do not copy these patterns into new code unless compatibility requires it.

## Existing authoritative documentation

* [`docs/example.md`](relative-link)

  * Covers ...
  * Treat as authoritative for ...
  * Does not cover ...
  * The section about ... appears stale because ...

## Known ambiguity and technical debt

* ...

## Evidence and verification

This skill was verified against commit `<commit>`.

Primary evidence:

* [`path`](relative-link)
* [`path`](relative-link)

````

## Description rules

The front-matter description is a routing instruction.

Weak:

```text
Documentation for authentication.
````

Strong:

```text
Use when changing login, session handling, token validation, protected routes,
identity-provider configuration, or authentication middleware.
```

## Scope rules

Scope is a routing aid.

It may contain:

* directories;
* files;
* globs;
* named infrastructure areas.

Do not imply exclusive ownership merely because a path appears in scope.

## Invariant rules

Invariants must be concrete and repository-specific.

Strong:

```text
Every tenant-scoped query must include the resolved tenant identifier.
```

Weak:

```text
Use good security practices.
```

## Workflow rules

Include only repository-supported workflows.

When practices conflict:

* describe the observed alternatives;
* identify the preferred current example;
* explain why;
* record remaining uncertainty.

## Commands

Only include verified commands found in:

* manifests;
* task files;
* CI configuration;
* scripts;
* current documentation confirmed against the repository.

Prefer scoped commands over unnecessarily running the entire repository suite.

## Evidence

Link representative evidence, not every file.

Prefer:

* entry points;
* important implementation;
* tests;
* contracts;
* configuration;
* scripts;
* deployment definitions;
* authoritative documentation.
