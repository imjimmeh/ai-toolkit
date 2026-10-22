# Bootstrap orchestration

## Overview

The bootstrap is a coordinator-led process.

Subagents gather evidence and return structured findings. The coordinator
synthesises those findings into a coherent knowledge model and skill catalogue.

Do not allow the process to become a recursive documentation exercise.

## Phase 1: Establish the analysis charter

Inspect enough of the repository to determine:

- repository root;
- repository type;
- current Git commit;
- default branch where detectable;
- primary languages;
- workspace and package managers;
- build systems;
- test frameworks;
- repository size;
- major framework signatures;
- existing documentation;
- existing agent instructions;
- generated directories;
- vendored code;
- archival or legacy areas;
- external systems required for understanding;
- output locations;
- available harness capabilities;
- analysis limitations.

Create:

```text
.agents/skills/knowledge/analysis-charter.yaml
````

Use the schema in the shared schemas reference.

Do not begin broad skill generation until the charter exists.

## Phase 2: Map the repository structurally

Launch a repository cartographer.

For very large repositories, split the cartography by major top-level area, such
as:

* applications;
* packages;
* infrastructure;
* tooling;
* data;
* test systems.

Merge all cartography centrally.

The map must identify:

* applications;
* services;
* workers;
* command-line tools;
* libraries;
* shared packages;
* infrastructure;
* deployment definitions;
* data stores;
* migrations;
* tests;
* developer tooling;
* code generation;
* API contracts;
* external integrations;
* documentation;
* generated artefacts;
* deprecated or archived areas.

For each structural unit, capture:

* identifier;
* type;
* path;
* responsibility;
* technologies;
* entry points;
* build, test, and run commands;
* deployability;
* direct dependencies;
* known consumers;
* external systems;
* data stores;
* related documentation;
* lifecycle status;
* confidence;
* evidence.

Create:

```text
.agents/skills/knowledge/repository-map.yaml
```

Do not create one skill per mapped unit.

## Phase 3: Audit existing documentation

Launch the documentation auditor in parallel with, or immediately after, the
cartographer.

Inspect:

* root documentation;
* application and package READMEs;
* architecture documents;
* ADRs;
* runbooks;
* onboarding material;
* deployment guides;
* API documentation;
* schema documentation;
* inline architectural comments;
* current agent instructions.

For each significant document, determine:

* subject;
* intended audience;
* likely authority;
* freshness;
* verified claims;
* conflicts;
* omissions;
* whether generated skills should link to it;
* whether it should be treated as canonical.

Create:

```text
.agents/skills/knowledge/documentation-audit.md
```

Do not mark a document stale based solely on age.

## Phase 4: Select focused investigations

Review the repository map and documentation audit.

Choose investigations across these dimensions:

### Structural

Examples:

* public web application;
* administration application;
* API;
* worker;
* infrastructure platform.

### Domain

Examples:

* identity;
* accounts;
* products;
* billing;
* search;
* content;
* localisation;
* notifications.

### Cross-cutting

Examples:

* authentication;
* authorisation;
* configuration;
* persistence;
* messaging;
* caching;
* feature flags;
* error handling;
* observability;
* API conventions;
* validation.

### Operational

Examples:

* local development;
* deployments;
* releases;
* rollback;
* migrations;
* environment provisioning;
* scheduled jobs;
* production diagnosis.

### Workflow

Examples:

* add an endpoint;
* add a database migration;
* create a domain module;
* add a locale;
* add an integration;
* add a background job;
* publish a package.

### Specialist and high-risk

Examples:

* payments;
* permissions;
* tenancy isolation;
* cryptography;
* search indexing;
* generated clients;
* legacy migration layers;
* destructive data processing.

Group investigations where concerns are tightly related.

Do not create separate investigations for tiny packages unless they have unusual
risk or project-specific behaviour.

## Phase 5: Build the concern map

Merge the focused investigation results into:

```text
.agents/skills/knowledge/concern-map.yaml
```

The concern map must represent relationships that the directory tree cannot.

For each concern, record:

* category;
* summary;
* implementation locations;
* related structural units;
* entry points;
* upstream and downstream dependencies;
* external systems;
* related concerns;
* common changes;
* invariants;
* risk;
* documentation;
* confidence;
* evidence.

A concern may span several structural units.

A structural unit may participate in several concerns.

## Phase 6: Produce candidate skills

Use the maps and audits to identify possible skills.

Candidate types:

* orientation;
* application;
* domain;
* cross-cutting;
* workflow;
* operations;
* specialist.

Score every candidate using the shared skill-selection reference.

Create:

```text
.agents/skills/knowledge/skill-catalogue.yaml
```

Record candidates that are:

* approved;
* merged;
* included as a parent section;
* represented by an existing documentation link;
* index-only;
* rejected;
* deferred.

Do not discard rejected candidates silently.

## Phase 7: Consolidate the catalogue

Before deep investigation, review candidate overlap.

Merge candidates when:

* they are always used together;
* they describe the same flow from different structural perspectives;
* one is an implementation detail of the other;
* they repeat the same invariants and validation;
* neither is independently actionable.

Separate candidates when:

* agents would load them for different tasks;
* their risks or invariants differ;
* their validation differs;
* they can change independently;
* combining them would produce a broad, difficult-to-route skill.

The coordinator makes the final decision.

## Phase 8: Deeply investigate approved skills

Launch focused skill investigators for each approved skill or closely related
group.

Each investigator returns a dossier conforming to the shared dossier schema.

The dossier must cover:

* use triggers;
* exclusions;
* scope;
* responsibilities;
* architecture;
* terminology;
* entry points;
* dependencies;
* flows;
* invariants;
* common change workflows;
* tests;
* operations;
* mistakes;
* legacy patterns;
* existing documentation;
* uncertainty;
* confidence;
* evidence.

Do not allow investigators to generate disconnected prose without structured
evidence.

## Phase 9: Generate project skills

Use the shared skill template.

Write each skill to:

```text
.agents/skills/<skill-id>/SKILL.md
```

Exactly one directory level under the skill root. Never group skills under an
intermediate directory; harnesses do not discover them there.

Each skill must:

* have a routing-oriented description;
* state when to use and not use it;
* define responsibilities and boundaries;
* explain meaningful architecture;
* include project terminology;
* identify representative entry points;
* state invariants;
* describe supported common workflows;
* specify validation;
* document operational consequences;
* warn about mistakes and legacy patterns;
* link existing authoritative documentation;
* record ambiguity;
* cite evidence;
* record verification commit and date.

## Phase 10: Create the project router

Create the top-level project skill at:

```text
.agents/skills/project/SKILL.md
```

It must route by:

* task;
* path;
* concept;
* affected application;
* related cross-cutting concern.

It should instruct future agents to load all materially relevant skills rather
than selecting exactly one.

The router should also explain what to do when:

* no skill matches;
* a skill appears stale;
* a skill contradicts current code;
* a path referenced by a skill no longer exists.

## Phase 11: Record unresolved questions

Create:

```text
.agents/skills/knowledge/unresolved-questions.md
```

Record material uncertainty including:

* question;
* why it matters;
* affected skills;
* inspected evidence;
* current inference;
* confidence;
* how it can be resolved;
* whether it blocks safe work.

Do not treat unresolved questions as failures.

Visible uncertainty is preferable to invented certainty.

## Phase 12: Review and validate

Launch the catalogue reviewer.

Apply targeted corrections.

Then run the checks from the shared validation reference.

Do not declare success while material unsupported claims remain.

## Phase 13: Completion report

Create:

```text
.agents/skills/knowledge/bootstrap-report.md
```

Include:

* repository summary;
* analysed scope;
* limitations;
* map statistics;
* candidate statistics;
* generated skills;
* merged and rejected candidates;
* documentation conflicts;
* significant unresolved questions;
* validation result;
* recommended future maintenance triggers.
