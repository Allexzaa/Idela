# [F001] — [Feature Name]

**Status:** Draft | In Review | Approved | In Build | Complete
**Phase:** [N]
**Last Updated:** [date]

---

## Header

**Sources:**
[Which architecture documents cover this phase — list file paths]

**Decisions:**
[Which ADR IDs constrain this phase — e.g., ADR-001, ADR-003]

**Constraints:**
[What the build order says this phase must NOT include]

**Deferred Items:**
[What is explicitly deferred from this phase and to which phase]

---

## Overview

[One paragraph. What this feature is and what it delivers for the user.]

---

## Scope

**In scope:**
- [Specific capability or behavior included in this feature]

**Out of scope:**
- [Specific thing that could be expected but is explicitly excluded]

---

## Requirements

### Functional Requirements

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-01 | | Must / Should / Could |
| FR-02 | | |

### Non-Functional Requirements

[Performance, security, or quality requirements specific to this feature,
beyond what is already in architecture/08-quality.md]

---

## User Flows

### Flow 1 — [Flow Name]

```
Actor: [who]
Precondition: [what must be true before this flow starts]

1. [step]
2. [step]
3. [step]

Outcome: [what the user experiences at the end]
```

### Error Cases

| Situation | System response |
|-----------|----------------|
| | |

---

## API Changes

[List only endpoints added or modified by this feature.
Full contracts are in architecture/05-api-contracts.md.]

| Method | Path | Change type | Notes |
|--------|------|-------------|-------|
| | | New / Modified | |

---

## Data Model Changes

[List only schema changes introduced by this feature.
Full model is in architecture/04-data-model.md.]

| Change | Table | Details |
|--------|-------|---------|
| | | New table / New field / New index |

---

## Acceptance Criteria

Derived from the release gate for this phase in architecture/09-build-order.md.

- [ ] [Specific, observable, testable criterion]
- [ ] [Specific, observable, testable criterion]
- [ ] All unit tests pass
- [ ] All integration tests pass
- [ ] Manual verification of [specific flow] completed

---

## What Comes Next

**Next feature:** [F00N] — [name]
**What this feature unlocks:** [what the next feature depends on from this one]

---

## Notes and Open Questions

| Question | Status | Resolution |
|----------|--------|------------|
| | Open / Resolved | |
