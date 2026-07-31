# Brownfield repository discovery

## Initial search targets

Search for repository guidance and high-level configuration before analysing
implementation details.

Common files include:

```text
AGENTS.md
CLAUDE.md
README*
CONTRIBUTING*
ARCHITECTURE*
SECURITY*
CODEOWNERS
docs/**
adr/**
decisions/**
.github/copilot-instructions.md

package.json
pnpm-workspace.yaml
yarn.lock
package-lock.json
turbo.json
nx.json
lerna.json

Cargo.toml
go.mod
go.work
pom.xml
build.gradle*
settings.gradle*
*.sln
*.csproj
Directory.Build.*

pyproject.toml
requirements*.txt
Pipfile
poetry.lock

Dockerfile*
docker-compose*
compose*.yaml
helm/**
charts/**
kubernetes/**
terraform/**
infrastructure/**
infra/**

.github/workflows/**
azure-pipelines*
.gitlab-ci*
Jenkinsfile

Makefile
Taskfile*
justfile
````

This list is illustrative, not exhaustive.

## Generated and external areas

Common generated or external directories include:

```text
node_modules
vendor
dist
build
coverage
.next
out
target
bin
obj
generated
.gen
cache
tmp
```

Do not exclude a directory based on name alone.

Verify using:

* generator configuration;
* file headers;
* build scripts;
* source-control patterns;
* package manifests;
* repository documentation.

Generated code may still need a specialist skill when agents must modify the
source schema or generator rather than the generated output.

## Repository-size strategy

### Small repository

A single cartographer may inspect the repository.

Typical characteristics:

* one or two deployables;
* limited package structure;
* straightforward build system;
* few cross-cutting concerns.

### Medium repository

Use separate investigation passes for:

* structural inventory;
* documentation;
* major applications;
* cross-cutting concerns;
* workflows.

### Large monorepo

First map workspace metadata and deployables.

Then group investigation by coherent area, such as:

```text
Customer-facing applications
Internal applications
Domain packages
Platform packages
Data and integration
Infrastructure and delivery
Testing and developer tooling
```

Do not launch hundreds of package-level subagents.

## Detecting structural units

Use multiple signals:

* workspace manifests;
* build targets;
* package manifests;
* executable entry points;
* deployment configuration;
* container definitions;
* CI jobs;
* import relationships;
* README descriptions;
* test projects;
* ownership rules.

A folder is not automatically a structural unit.

A structural unit should have a meaningful responsibility, lifecycle, build
boundary, deployment boundary, or dependency role.

## Detecting domains

Look for recurring business terminology across:

* types;
* schemas;
* route names;
* database tables;
* events;
* tests;
* UI features;
* API contracts;
* package names;
* documentation.

Follow concepts across packages.

Do not assume a directory named `domain` represents the complete business
domain.

## Detecting workflows

Look for repeated change shapes in:

* recent commits;
* pull-request conventions where available;
* tests;
* scaffolding;
* scripts;
* code generators;
* similar features;
* migrations;
* CI validation.

A workflow is a strong skill candidate when agents must modify several places in
a particular order.

## Detecting risk

Risk indicators include:

* authentication or permissions;
* security boundaries;
* destructive data operations;
* payment or financial behaviour;
* compliance-sensitive output;
* tenancy isolation;
* cross-region behaviour;
* migration compatibility;
* deployment sequencing;
* distributed consistency;
* public API compatibility;
* external indexes;
* manually operated scripts;
* sparse tests;
* unclear ownership;
* duplicate legacy and current implementations.

Risk alone may justify a skill even when modification frequency is low.

## Detecting legacy code

Signals include:

* deprecated annotations;
* compatibility names;
* duplicate implementations;
* old framework versions isolated to one area;
* archive directories;
* migration adapters;
* comments referring to temporary transitions;
* build exclusions;
* absence from current dependency paths;
* recent history that only removes code;
* documentation describing replacement systems.

Do not declare code unused without stronger evidence.

Use terms such as:

* active;
* legacy but active;
* compatibility-only;
* deprecated;
* apparently unused;
* status unknown.

## Git history

Use history when available to understand:

* files commonly changed together;
* preferred current examples;
* recently replaced patterns;
* ownership;
* recurring workflows;
* architectural migrations.

Do not treat frequency as proof of architectural importance.

Do not assume old patterns remain preferred.

Prefer recent representative changes that align with current code and tests.
