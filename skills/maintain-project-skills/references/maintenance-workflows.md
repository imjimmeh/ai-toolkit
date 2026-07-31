# Project-skill maintenance workflows

## Targeted refresh

Use when an existing skill is materially stale in a bounded area.

### Process

1. Read the skill and its catalogue entry.
2. Read relevant repository-map and concern-map entries.
3. identify the skill's verification commit.
4. Inspect relevant changes since that commit.
5. Verify current paths, entry points, commands, invariants, and workflows.
6. Determine whether related skills are affected.
7. Update the relevant evidence dossier or reconstruct one.
8. Update the skill.
9. Update routing and cross-links where needed.
10. Update unresolved questions.
11. Validate the affected scope.

### Avoid

- updating unrelated skill wording;
- changing all verification commits;
- replacing the skill based only on a single changed file;
- preserving claims that can no longer be supported.

## Add a new skill

Use when an important concern is absent from the catalogue.

### Process

1. Search the catalogue for overlapping skills.
2. Determine whether the concern belongs in an existing skill.
3. Score the candidate using the shared selection rules.
4. Record the candidate and decision.
5. Run a focused skill investigation.
6. Generate the skill using the shared template.
7. Add routing by task, path, and concept.
8. Add related-skill links.
9. Update the concern map and repository map where necessary.
10. Validate.

Do not create a new skill merely because a new package was added.

## Audit the catalogue

Use when the user asks for quality, freshness, consistency, or coverage review.

Check:

- missing major concerns;
- obsolete skills;
- broken paths;
- invalid commands;
- duplicated knowledge;
- contradictory claims;
- over-broad skills;
- excessively narrow skills;
- weak activation descriptions;
- missing invariants;
- missing validation guidance;
- stale documentation links;
- unsupported claims;
- inconsistent terminology;
- incorrect verification metadata.

An audit may recommend changes without applying them when the user requested
review only.

## Merge skills

Merge when:

- both are always loaded together;
- one is only an implementation detail of the other;
- they duplicate architecture, invariants, and validation;
- repository changes removed the original boundary;
- separate routing no longer helps agents.

### Process

1. Choose the canonical surviving skill ID.
2. Combine unique useful content.
3. Remove duplicated content.
4. preserve distinct workflows where they remain useful.
5. Update scope and routing.
6. Update incoming related-skill references.
7. Mark the removed catalogue entry as merged.
8. Remove or archive the redundant skill according to repository convention.
9. Validate links and routing.

Do not simply concatenate the two skill files.

## Split a skill

Split when:

- agents load it for materially different tasks;
- it contains unrelated concerns;
- component areas have different risks;
- component areas have different tests or operations;
- one part can change independently;
- routing has become vague;
- the document has become too broad to be actionable.

### Process

1. Define the new conceptual boundaries.
2. Score each proposed child skill.
3. Identify shared knowledge that belongs in a parent or cross-cutting skill.
4. Run focused investigations for each child.
5. Create the new skills.
6. reduce or retire the original skill.
7. Update routing and related links.
8. Record the split in the catalogue.
9. Validate.

Do not divide solely to shorten a long file.

## Retire a skill

Retire when the concern no longer exists or is no longer independently useful.

### Process

1. Verify the concern is removed, replaced, or absorbed.
2. Search for incoming router and related-skill references.
3. Determine whether any historical guidance remains operationally relevant.
4. Remove the skill from active routing.
5. Update or remove the catalogue entry.
6. Redirect agents to the replacement skill where applicable.
7. Preserve warnings only where compatibility code remains.
8. Validate that no active path points to the retired skill.

Do not declare code unused from naming or age alone.

## Routing repair

Use when skills are accurate but agents cannot reliably select them.

Improve:

- description metadata;
- path globs;
- concept keywords;
- task examples;
- related-skill references;
- top-level task routing;
- application routing.

Avoid broad keywords that cause nearly every task to match.

## Documentation reconciliation

Use when project skills and existing documentation disagree.

### Process

1. Identify the exact conflicting claims.
2. Check implementation, tests, runtime configuration, recent ADRs, and history.
3. Determine which source is currently authoritative.
4. Update the skill.
5. Record the documentation conflict.
6. Link the document with a clear freshness warning where still useful.
7. Do not edit the original project documentation unless requested.

## Partial verification

Sometimes only a narrow section can be confidently updated.

In that case:

- do not update the global verification commit unless the full skill was checked;
- add a note identifying the newly verified section and commit;
- retain older verification metadata for untouched sections where the format
  supports it;
- consider splitting the skill if partial verification repeatedly becomes
  difficult.

## Escalation to full bootstrap

Recommend or invoke the full bootstrap only when:

- the router and catalogue are missing or unusable;
- repository structure has fundamentally changed;
- most skills are materially stale;
- maps are absent and targeted maintenance cannot determine impact;
- catalogue boundaries no longer resemble the repository;
- a partial update would be more expensive or misleading than reanalysis.

Record why full bootstrap is necessary.