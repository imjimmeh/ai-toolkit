# Skill candidate selection

## What deserves a skill

A concern is a stronger skill candidate when several of these are true:

- it is changed frequently;
- it has non-obvious architecture;
- it spans packages, layers, applications, or operational systems;
- mistakes have meaningful blast radius;
- it has project-specific invariants;
- it requires a particular sequence of changes;
- it has distinct validation;
- it has operational consequences;
- documentation is missing, fragmented, or stale;
- agents are likely to encounter it as a coherent task;
- it contains preferred and legacy patterns that are difficult to distinguish.

A concern may deserve a skill based on high risk even when changed infrequently.

## What usually does not deserve a skill

A standalone skill is usually unnecessary when:

- the package is tiny and self-explanatory;
- an existing current document already provides sufficient agent guidance;
- the code is generated and agents should not edit it directly;
- it is a generic wrapper with no project-specific behaviour;
- the content would be only an API or file listing;
- it duplicates another skill;
- it is unlikely to be modified directly;
- it has no meaningful decisions, invariants, workflow, or validation.

## Candidate types

Use:

```text
orientation
application
domain
cross-cutting
workflow
operations
specialist
````

### Orientation

Broad repository entry points.

Examples:

* repository overview;
* architecture;
* local development;
* testing strategy.

### Application

A substantial deployable or executable unit with a coherent operating model.

### Domain

A business capability with meaningful terminology and invariants, potentially
spanning several structural units.

### Cross-cutting

A technical concern spanning applications or packages.

Examples:

* authentication;
* persistence;
* configuration;
* observability.

### Workflow

A recurring project-specific sequence for making a change.

Examples:

* add a locale;
* add an endpoint;
* add a migration.

### Operations

A runtime or delivery process.

Examples:

* deployment;
* rollback;
* reindexing;
* environment provisioning.

### Specialist

A high-risk, unusual, legacy, generated, or otherwise specialised subsystem.

## Candidate scoring

Score each category from 0 to 3.

### Modification frequency

```text
0: almost never changed directly
1: occasionally changed
2: regularly changed
3: central to frequent repository work
```

### Complexity

```text
0: self-explanatory
1: modest local complexity
2: non-obvious architecture or workflow
3: substantial investigation required
```

### Cross-boundary reach

```text
0: one obvious file or package
1: local package with limited dependencies
2: several packages or layers
3: multiple applications, services, or operational systems
```

### Risk

```text
0: low-consequence changes
1: localised failure risk
2: meaningful functional or operational risk
3: high blast radius, security, data, compliance, or production risk
```

### Documentation gap

```text
0: current authoritative guidance exists
1: adequate guidance with minor gaps
2: fragmented or partially stale guidance
3: important knowledge is undocumented
```

### Project specificity

```text
0: generic framework behaviour
1: mostly generic
2: materially project-specific
3: strongly dependent on repository-specific design
```

### Agent usefulness

```text
0: unlikely to affect decisions
1: occasional background value
2: likely to improve implementation quality
3: essential for safe or correct work
```

## Weighted score

```text
modification_frequency * 1
complexity            * 2
cross_boundary_reach  * 2
risk                   * 3
documentation_gap     * 1
project_specificity   * 2
agent_usefulness      * 3
```

Maximum: 42.

Default interpretation:

```text
30–42: strong dedicated-skill candidate
22–29: dedicated skill or major section, subject to overlap review
14–21: usually merge into a broader skill
0–13: documentation link, index entry, or no generated skill
```

The score guides judgement. It does not replace it.

## Candidate decisions

Use:

```text
dedicated-skill
merge-into
section-in-parent
documentation-link-only
index-entry-only
rejected
deferred
retired
```

Always record the reason for non-dedicated decisions.

## Boundary tests

Before approving a candidate, ask:

1. Would an agent load this for a coherent class of tasks?
2. Does it contain distinct decisions, invariants, or validation?
3. Is its scope understandable without relying on a folder name?
4. Does it duplicate another candidate?
5. Would merging it make the parent confusing?
6. Would splitting it improve routing or merely shorten the file?
7. Can its important claims be supported?

## Workflow versus domain

Prefer a workflow skill when:

* the order of changes matters;
* several areas change together;
* the same task recurs;
* validation is project-specific;
* agents might copy obsolete examples.

Prefer a domain skill when:

* business meaning and invariants are central;
* the concern spans implementations;
* many different workflows operate on the same model.

A repository may need both.

The workflow skill should link to the domain skill instead of duplicating domain
architecture.

## Application versus cross-cutting

Prefer an application skill when most relevant knowledge is local to one
deployable.

Prefer a cross-cutting skill when agents must follow the concern across several
applications, packages, or operational boundaries.

## Maximum catalogue size

Do not enforce a hard maximum.

Treat unusually large catalogues as a signal to review:

* duplicate boundaries;
* package-level over-documentation;
* weak candidate thresholds;
* missing parent skills;
* overly specific workflow skills.
