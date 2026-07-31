# Evidence and confidence

## Evidence hierarchy

Use this default hierarchy when sources disagree:

1. executable tests that exercise the relevant current behaviour;
2. runtime and build configuration;
3. current implementation;
4. API, event, and data schemas;
5. recent architectural decision records;
6. maintained project documentation;
7. package documentation;
8. recent Git history;
9. naming and directory structure.

This hierarchy is guidance, not an absolute rule.

Tests may encode obsolete behaviour.

Configuration may describe an environment that is no longer deployed.

Implementation may contain dead code.

Resolve contradictions rather than blindly selecting the highest-ranked source.

## Evidence requirements

Important claims should identify representative repository evidence.

Examples of important claims:

- ownership boundaries;
- security or permission behaviour;
- data flow;
- deployability;
- migration compatibility;
- public API behaviour;
- common change workflow;
- required validation;
- production consequences;
- legacy status;
- external integration behaviour.

A skill does not need a citation after every sentence.

It must provide enough evidence that another agent can verify consequential
claims.

## Fact, inference, and uncertainty

Distinguish:

### Verified fact

Directly supported by current code, tests, configuration, or authoritative
documentation.

Example:

```text
The API rejects requests without a tenant identifier before the domain handler
is invoked.
````

Evidence:

* middleware implementation;
* middleware tests;
* route registration.

### Strong inference

Supported by several signals but not directly confirmed.

Example:

```text
The legacy importer appears to be manually operated rather than scheduled.
```

Evidence:

* script exists;
* no active workflow references it;
* recent commits update it occasionally.

### Unresolved ambiguity

Evidence conflicts or is insufficient.

Example:

```text
It is unclear whether the compatibility endpoint remains used by external
customers.
```

## Confidence levels

### High

Use when:

* important behaviour is directly confirmed;
* tests and implementation agree;
* configuration supports the described runtime model;
* no material contradictory evidence exists.

### Medium

Use when:

* the model is well supported;
* some behaviour is inferred;
* one external dependency or operational detail cannot be inspected;
* minor documentation conflicts remain.

### Low

Use when:

* important behaviour is ambiguous;
* repository evidence conflicts;
* external systems determine key behaviour;
* code may be legacy or unused;
* tests are absent in consequential areas;
* ownership is unclear.

## Evidence records

Use evidence entries such as:

```yaml
evidence:
  - path: apps/api/src/auth/token-validator.ts
    supports: Token validation rules and issuer checks
    kind: implementation

  - path: apps/api/src/auth/token-validator.test.ts
    supports: Rejection behaviour for invalid issuers
    kind: test

  - path: docs/authentication.md
    supports: Identity-provider terminology
    kind: documentation
    freshness: partially-stale
```

Allowed evidence kinds may include:

```text
implementation
test
configuration
schema
documentation
history
script
workflow
manifest
deployment
```

## Existing documentation

When linking existing documentation, explain:

* what it covers;
* what it is authoritative for;
* what it omits;
* whether any section is stale;
* which current evidence contradicts it.

Weak:

```text
See docs/auth.md.
```

Strong:

```text
`docs/auth.md` is the primary source for identity-provider terminology and token
lifetimes. Its local-development commands are stale; use the scripts in
`apps/api/package.json`.
```

## Sensitive evidence

Do not reproduce:

* secrets;
* private keys;
* tokens;
* credentials;
* production personal data;
* protected customer information.

Reference secure configuration locations without including values.
