# Project-skill validation

## Required checks

Validate both the human-readable skills and the supporting knowledge artefacts.

## Structural checks

Confirm:

- every generated skill has front matter;
- every skill ID is unique;
- every approved catalogue entry has a skill file;
- every generated skill has a catalogue entry;
- the project router exists;
- the router lists all active skills;
- merged and rejected candidates have reasons;
- retired skills are not actively routed.

## Reference checks

Confirm:

- related skill IDs exist;
- repository-relative links resolve;
- referenced files exist or are explicitly historical;
- path globs are plausible;
- documentation links exist;
- no absolute local-machine paths appear;
- no secret values were copied.

## Command checks

Confirm every command appears in one or more of:

- package manifest;
- task runner;
- build configuration;
- CI workflow;
- repository script;
- current verified documentation.

Do not execute destructive commands merely to validate them.

## Evidence checks

Confirm:

- consequential claims have representative evidence;
- inferences are labelled;
- uncertainty is recorded;
- claims are not based solely on names;
- documentation conflicts are visible;
- legacy status is appropriately qualified.

## Skill quality checks

Every skill should have:

- useful activation guidance;
- exclusions;
- coherent responsibilities;
- meaningful boundaries;
- project-specific architecture or workflow;
- invariants;
- validation;
- hazards or common mistakes where relevant;
- existing documentation references;
- evidence;
- verification metadata.

Reject skills that merely list files or restate package names.

## Routing checks

Test representative tasks against the router.

Examples:

```text
Add a protected API endpoint
Change product availability for one market
Add a database migration
Modify deployment environment variables
Investigate failed search indexing
Add a new locale
````

For each task, confirm that the router identifies:

* the main domain or application skill;
* relevant workflow skills;
* relevant cross-cutting skills;
* operational skills where consequences exist.

The router should allow several skills to match.

## Freshness checks

Confirm:

* verification commits exist;
* verification dates are valid;
* skills updated incrementally do not claim broader verification than performed;
* unaffected skills were not stamped with the current commit without review.

## Contradiction review

Search for repeated key claims across skills, including:

* ownership;
* data source of truth;
* authentication boundaries;
* deployment responsibility;
* migration order;
* configuration precedence;
* public visibility rules;
* event ownership;
* external integration direction.

Where duplication is necessary, identify one canonical skill and make other
skills link to it.

## Automated validation suggestions

Where supported, implement scripts to check:

* YAML front matter;
* unique names;
* related-skill references;
* catalogue-to-file correspondence;
* relative links;
* repository paths;
* consistent verification metadata;
* empty sections;
* placeholder markers such as `<...>`.

Do not treat automated checks as a substitute for conceptual review.

## Validation result

Use:

```text
passed
passed-with-warnings
failed
```

A warning is appropriate for:

* unresolved external operational behaviour;
* a possibly active legacy path;
* unavailable production configuration;
* a documentation conflict that does not block safe local work.

Failure is appropriate for:

* missing approved skills;
* broken router references;
* unsupported high-risk claims;
* contradictory invariants;
* invalid validation commands;
* misleading verification metadata;
* unresolved ambiguity that prevents safe work.

## Review report

The validation report should state:

* scope;
* skills checked;
* checks performed;
* warnings;
* blockers;
* files not revalidated;
* final status.

```