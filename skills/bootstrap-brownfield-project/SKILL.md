---
name: bootstrap-brownfield-project
description: >
  Analyse an existing brownfield repository and create an initial catalogue of
  project-specific agent skills. Use when a substantial repository has no
  reliable project skill catalogue, when the user explicitly requests initial
  repository skill generation, or when existing agent documentation is too
  limited to support safe work.
---

# Bootstrap Brownfield Project

## Purpose

Create an evidence-based catalogue of project-specific skills that future coding
agents can consult before changing the repository.

The resulting catalogue should help an agent understand:

- what exists in the repository;
- how major parts of the system relate;
- which business and technical concerns cross structural boundaries;
- which invariants must remain true;
- how common changes are performed;
- which tests and validation steps are required;
- which areas are risky, legacy, generated, or poorly understood;
- which existing documents are authoritative;
- which specialised project skills should be loaded for a task.

This skill is primarily intended for a deliberate initial run on an existing
repository.

Do not use it for routine updates to an existing healthy skill catalogue. Use
`maintain-project-skills` for incremental work.

## Read before starting

Read these shared references:

1. `../project-skill-toolkit/references/evidence-and-confidence.md`
2. `../project-skill-toolkit/references/skill-selection.md`
3. `../project-skill-toolkit/references/schemas.md`
4. `../project-skill-toolkit/references/subagent-prompts.md`
5. `../project-skill-toolkit/references/skill-template.md`
6. `../project-skill-toolkit/references/validation.md`

Read these bootstrap-specific references:

1. `references/orchestration.md`
2. `references/discovery.md`

## Core objective

Optimise for this question:

> What does an agent need to know to safely make a meaningful change?

Do not optimise for:

> How can every directory and package be described?

The repository structure is an input to the analysis. It must not automatically
determine the final skill boundaries.

## Operating constraints

### Do not modify product code

This skill creates documentation, maps, catalogues, and agent skills.

Do not:

- refactor application code;
- upgrade dependencies;
- repair unrelated tests;
- change runtime behaviour;
- alter infrastructure;
- deploy;
- publish packages;
- apply migrations.

Record discovered issues without fixing them unless the user separately asks.

### Protect sensitive information

Do not copy secret values, credentials, access tokens, private keys, personal
data, production connection strings, or private operational details into
generated skills.

Document secret-handling mechanisms and relevant paths without including secret
values.

### Follow repository-local instructions

Before writing files, search for and follow repository guidance such as:

- `AGENTS.md`
- `CLAUDE.md`
- `.github/copilot-instructions.md`
- contribution guides;
- repository-specific skill conventions;
- documentation placement rules.

If an established project-skill directory already exists, adapt to it rather
than introducing a competing structure.

Record the chosen output structure in the analysis charter.

## Required outputs

Unless an established repository convention replaces them, create everything
under the repository's agent-skill root, `.agents/skills/`:

```text
./.agents/skills/
  project/
    SKILL.md

  <approved-skill>/
    SKILL.md

  knowledge/
    analysis-charter.yaml
    repository-map.yaml
    concern-map.yaml
    documentation-audit.md
    skill-catalogue.yaml
    unresolved-questions.md
    bootstrap-report.md
```

Skills sit directly under `.agents/skills/`, never under a grouping directory.
Harnesses discover skills non-recursively as `<skills-root>/<name>/SKILL.md`, so
`.agents/skills/project/<approved-skill>/SKILL.md` would never be discovered.
`knowledge/` holds no `SKILL.md` and is read by path instead.

The full layout, including the link base for repository files, is defined in
`../project-skill-toolkit/references/schemas.md`.

The process is incomplete until it has produced:

1. an analysis charter;
2. a structural repository map;
3. a concern map;
4. a documentation audit;
5. a scored and reviewed candidate skill catalogue;
6. one skill for each approved catalogue entry;
7. a top-level project router;
8. unresolved questions;
9. a validation result;
10. a bootstrap completion report.

## Execution phases

Follow the detailed orchestration in `references/orchestration.md`.

The required phases are:

1. establish the analysis charter;
2. map the repository structurally;
3. audit existing documentation;
4. identify domains, cross-cutting concerns, workflows, and risky areas;
5. create and score candidate skills;
6. consolidate candidate boundaries;
7. deeply investigate approved candidates;
8. generate the skill files;
9. create the top-level project router;
10. record unresolved questions;
11. review and validate the catalogue;
12. produce the completion report.

Do not skip candidate scoring and consolidation.

Do not launch one subagent per package before the structural map exists.

## Subagent use

Use subagents for bounded evidence-gathering and specialist investigation.

The coordinating agent owns:

* analysis boundaries;
* terminology;
* candidate skill selection;
* skill boundaries;
* deduplication;
* evidence standards;
* conflict resolution;
* final file generation;
* catalogue consistency.

Subagents should not independently decide the final catalogue structure.

Use the prompts in:

```text
../project-skill-toolkit/references/subagent-prompts.md
```

## Initial skill catalogue principles

A healthy initial catalogue often contains:

* repository overview;
* architecture and dependency boundaries;
* local development;
* testing strategy;
* configuration and environments;
* release and deployment;
* major deployable applications or services;
* major business domains;
* important cross-cutting concerns;
* external integrations;
* persistence and migrations;
* observability and diagnosis;
* common high-value change workflows;
* legacy areas and known hazards.

Do not force this exact list.

For a modest repository, approximately 8–15 initial skills is often reasonable.

For a large monorepo, approximately 12–25 may be reasonable.

These are warning ranges, not quotas.

## Completion criteria

The bootstrap is complete only when:

* all approved catalogue entries have skill files;
* all generated skill files have catalogue entries;
* rejected and merged candidates have recorded reasons;
* the top-level router can select skills by task, path, and concept;
* important claims are supported by evidence;
* uncertainty is visible;
* relative links resolve;
* referenced commands exist;
* verification commit metadata is consistent;
* the catalogue reviewer finds no material unsupported claims.

## Final response

Report:

* repository type;
* analysed scope;
* verification commit;
* structural units found;
* concerns found;
* candidate skills considered;
* skills generated;
* candidates merged or rejected;
* significant documentation conflicts;
* unresolved high-risk questions;
* validation status;
* output paths.
