---
name: maintain-project-skills
description: >
  Audit, update, extend, merge, split, or retire an existing catalogue of
  project-specific agent skills. Use when repository structure or behaviour has
  changed, a current task exposes missing or stale project knowledge, or the
  user requests a targeted skill-catalogue refresh.
---

# Maintain Project Skills

## Purpose

Keep an existing project-skill catalogue accurate, useful, and appropriately
scoped without rerunning a full brownfield bootstrap.

Use this skill to:

- refresh a skill affected by repository changes;
- add a skill for a newly introduced concern;
- document a previously uncovered area;
- update routing metadata;
- split an over-broad skill;
- merge overlapping skills;
- retire obsolete skills;
- audit catalogue consistency;
- repair broken paths, commands, or links;
- reconcile skills with current implementation.

Do not use this skill to perform the first full analysis of a substantial
undocumented repository. Use `bootstrap-brownfield-project` instead.

## Read before starting

Read these shared references:

1. `../project-skill-toolkit/references/evidence-and-confidence.md`
2. `../project-skill-toolkit/references/skill-selection.md`
3. `../project-skill-toolkit/references/schemas.md`
4. `../project-skill-toolkit/references/subagent-prompts.md`
5. `../project-skill-toolkit/references/skill-template.md`
6. `../project-skill-toolkit/references/validation.md`

Read:

```text
references/maintenance-workflows.md
````

## Invocation triggers

Use this skill when one or more of these are true:

* an existing skill references deleted or moved paths;
* current code materially contradicts a skill;
* a new application, service, domain, integration, or platform has appeared;
* a task affects an important concern absent from the catalogue;
* a major migration changes boundaries or workflows;
* several skills duplicate the same knowledge;
* one skill has become too broad;
* a skill describes a concern that no longer exists;
* the user asks for a catalogue audit or refresh;
* the same undocumented convention has repeatedly affected work.

Do not run merely because:

* a skill is a few commits old;
* an implementation detail changed;
* one example file moved;
* the current task is local and readily understood;
* a minor wording improvement is possible.

## Maintenance principle

Update the smallest coherent set of knowledge artefacts and skills necessary to
restore accuracy.

Do not rewrite unaffected skills.

Do not change an unaffected skill's `last_verified` commit unless it was
actually revalidated.

## Required inputs

Inspect, under the repository's agent-skill root (`.agents/skills/` by default):

* the project router at `project/SKILL.md`;
* the skill catalogue at `knowledge/skill-catalogue.yaml`;
* relevant skill files at `<skill-id>/SKILL.md`;
* repository map entries in `knowledge/repository-map.yaml`;
* concern map entries in `knowledge/concern-map.yaml`;
* unresolved questions in `knowledge/unresolved-questions.md`;
* current Git commit;
* changed files since relevant verification commits where available;
* current repository evidence.

The canonical layout is defined in
`../project-skill-toolkit/references/schemas.md`. If the repository records a
different skill root in its analysis charter, use that instead.

If one or more supporting knowledge files do not exist, reconstruct only what is
required for the requested maintenance.

Do not silently perform a full bootstrap unless the catalogue is unusable.

## Maintenance modes

Choose one or more:

```text
targeted-refresh
new-skill
catalogue-audit
merge-skills
split-skill
retire-skill
routing-repair
documentation-reconciliation
```

Record the chosen mode and affected scope.

## Required process

1. identify the maintenance trigger;
2. determine affected skills and knowledge artefacts;
3. inspect changes since the recorded verification commit;
4. assess whether the current skill boundary still makes sense;
5. run focused investigation;
6. update the minimum necessary maps and catalogue entries;
7. update, add, split, merge, or retire skills;
8. repair router entries and cross-links;
9. update unresolved questions;
10. validate the affected catalogue;
11. report exactly what changed and what was not revalidated.

## Subagent use

Use focused subagents when the affected concern is broad, cross-cutting,
ambiguous, or high-risk.

Do not launch full-repository cartography for a local maintenance task.

The coordinator owns:

* scope control;
* deciding which skills are affected;
* boundary changes;
* catalogue consistency;
* final validation.

## Verification metadata

When a skill is fully revalidated:

```yaml
last_verified:
  commit: <current-commit>
  date: <current-date>
```

When only part of a skill is updated, either fully revalidate the skill or record
more granular verification notes in the body.

Do not imply the entire skill was checked when only one paragraph was edited.

## Completion criteria

Maintenance is complete when:

* affected skill claims match current repository evidence;
* affected routing entries are accurate;
* related-skill references resolve;
* relevant maps and catalogue entries are consistent;
* obsolete references are removed or marked historical;
* verification metadata is honest;
* unresolved uncertainty is recorded;
* validation passes for the affected scope.

## Final response

Report:

* maintenance mode;
* trigger;
* affected skills;
* files changed;
* skills added, updated, merged, split, or retired;
* maps or catalogue entries updated;
* verification commits;
* unresolved questions;
* validation status;
* areas deliberately not revalidated.
