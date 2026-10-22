# Shared schemas

These schemas define expected structure. Repositories may add fields but should
retain the core semantics.

## Canonical output layout

Unless the repository already has an established agent-skill root, all output
lives under `.agents/skills/`:

```text
<repository-root>/
  .agents/
    skills/
      project/
        SKILL.md              # top-level project router
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

Two properties of this layout are load-bearing:

1. **Every skill is exactly one level under `.agents/skills/`.** Agent harnesses
   discover skills non-recursively as `<skills-root>/<skill-name>/SKILL.md`.
   A nested layout such as `.agents/skills/project/<id>/SKILL.md` is not
   discovered at all.
2. **`knowledge/` contains no `SKILL.md`.** It is inert data for agents to read
   by path, not a skill, and must not register as one.

Skill-to-skill links therefore stay `../<skill-id>/SKILL.md`. Links to
repository files use the link base defined in the skill template.

## Analysis charter

```yaml
schema_version: 1

repository:
  root: .
  type: monorepo
  current_commit: "<commit>"
  default_branch: "<branch-or-unknown>"

technology:
  languages:
    - name: typescript
      confidence: high
  package_managers:
    - pnpm
  build_systems:
    - turborepo
  test_frameworks:
    - vitest

analysis:
  mode: initial-bootstrap
  skill_root: .agents/skills
  knowledge_root: .agents/skills/knowledge

  include:
    - apps
    - packages
    - infrastructure

  exclude:
    - node_modules
    - dist

  excluded_reasoning:
    node_modules: external dependencies
    dist: generated build output

existing_guidance:
  - path: AGENTS.md
    role: repository-wide agent instructions

constraints:
  history_available: true
  external_services_available: false
  production_configuration_available: false

known_limitations: []
````

## Repository map

```yaml
schema_version: 1
verified_at_commit: "<commit>"

units:
  - id: web-app
    name: Web application
    type: application
    path: apps/web

    purpose: >
      Public-facing application.

    technologies:
      languages:
        - typescript
      frameworks:
        - nextjs

    entry_points:
      - apps/web/src/app
      - apps/web/next.config.ts

    commands:
      build:
        - pnpm --filter web build
      test:
        - pnpm --filter web test
      start:
        - pnpm --filter web dev

    deployable: true

    depends_on:
      - ui-library

    consumed_by: []

    external_integrations:
      - contentful

    data_stores: []

    documentation:
      - apps/web/README.md

    status:
      lifecycle: active
      confidence: high

    evidence:
      - path: apps/web/package.json
        supports: Build and test commands
        kind: manifest
```

Recommended unit types:

```text
application
service
worker
cli
library
package
infrastructure
database
migration
test-suite
tooling
code-generator
contract
documentation
generated
legacy
unknown
```

Recommended lifecycle values:

```text
active
legacy-active
compatibility-only
deprecated
apparently-unused
archived
generated
unknown
```

## Concern map

```yaml
schema_version: 1
verified_at_commit: "<commit>"

concerns:
  - id: product-catalogue
    name: Product catalogue
    category: domain

    summary: >
      Owns canonical product definitions, availability, catalogue queries,
      indexing projection, and presentation.

    implemented_in:
      - packages/product-domain
      - apps/admin/src/products
      - apps/web/src/features/products

    related_units:
      - web-app
      - admin-app
      - product-domain

    entry_points:
      - packages/product-domain/src/index.ts

    dependencies:
      upstream: []
      downstream:
        - search-indexing
      external:
        - contentful

    related_concerns:
      - localisation
      - search-indexing

    common_changes:
      - add a product field
      - alter regional availability

    invariants:
      - Public visibility must respect regional availability.

    risk:
      level: high
      reasons:
        - spans multiple deployables
        - external index synchronisation

    documentation:
      - docs/catalogue.md

    confidence: medium

    evidence:
      - path: packages/product-domain/src/product.ts
        supports: Canonical product model
        kind: implementation
```

Recommended categories:

```text
structural
domain
cross-cutting
operations
workflow
specialist
```

## Skill catalogue

```yaml
schema_version: 1
verified_at_commit: "<commit>"

catalogue:
  - id: authentication
    title: Authentication and session lifecycle
    type: cross-cutting

    summary: >
      Authentication architecture spanning web, API, middleware, sessions,
      token validation, and identity-provider configuration.

    proposed_scope:
      - apps/web/src/auth
      - apps/api/src/auth
      - packages/auth-client

    use_when:
      concepts:
        - authentication
        - login
        - session
        - token

      paths:
        - apps/web/src/auth/**
        - apps/api/src/auth/**
        - packages/auth-client/**

      tasks:
        - change sign-in behaviour
        - alter session handling
        - add a protected route

    scores:
      modification_frequency: 2
      complexity: 3
      cross_boundary_reach: 3
      risk: 3
      documentation_gap: 2
      project_specificity: 3
      agent_usefulness: 3
      weighted_total: 38

    decision: dedicated-skill

    decision_reason: >
      Spans multiple deployables and contains security-sensitive invariants.

    related_candidates:
      - authorisation
      - configuration

    assigned_investigation:
      status: complete
      source: concern-investigator-authentication

    evidence:
      - path: apps/api/src/auth/token-validator.ts
        supports: Token-validation behaviour
        kind: implementation
```

## Skill investigation dossier

```yaml
skill:
  id: product-catalogue
  title: Product catalogue
  type: domain

  purpose: >
    Help agents safely modify product definitions, availability, catalogue
    queries, indexing, and product presentation.

  use_when:
    paths: []
    concepts: []
    tasks: []

  do_not_use_when: []

  scope:
    included: []
    excluded: []

  responsibilities: []

  terminology:
    - term: product availability
      meaning: >
        Regional decision determining whether a canonical product is visible.

  architecture:
    summary: ""
    components: []
    flows: []

  entry_points: []

  dependencies:
    upstream: []
    downstream: []
    external: []

  invariants: []

  common_workflows:
    - name: Add a product field
      steps: []
      files_commonly_changed_together: []
      validation: []

  testing:
    required: []
    conditional: []

  operations: []

  hazards: []

  legacy_patterns: []

  documentation:
    - path: docs/catalogue.md
      authority: primary
      covers: []
      omissions: []
      freshness: current

  unresolved_questions: []

  confidence: high

  evidence: []
```

## Unresolved question

```yaml
question: Is the legacy importer still used in production?
why_it_matters: >
  It bypasses the current validation pipeline.
affected_skills:
  - product-catalogue
  - persistence-and-migrations
evidence_inspected:
  - scripts/import-products.ts
  - .github/workflows
current_inference: >
  It may be manually operated, but no active scheduled workflow references it.
confidence: low
resolution: >
  Confirm with the owning team or inspect production job configuration.
blocking: true
```

## Validation report

```yaml
validation:
  status: passed-with-warnings

  scope:
    mode: initial-bootstrap
    skills_checked:
      - project
      - authentication
      - product-catalogue

  statistics:
    candidates: 24
    approved: 12
    generated: 12
    merged: 7
    rejected: 5

  checks:
    front_matter: passed
    unique_ids: passed
    catalogue_coverage: passed
    related_skill_references: passed
    repository_paths: passed-with-warnings
    commands: passed
    relative_links: passed
    verification_metadata: passed
    unresolved_questions: passed

  warnings:
    - skill: product-catalogue
      issue: Production use of legacy importer could not be verified

  blockers: []
```
