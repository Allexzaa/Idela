# Architecture Decision Records — Index

All significant architectural decisions are recorded here.
ADRs are append-only. Superseded ADRs are never deleted — a new ADR supersedes them.

---

## Index

| ID | Title | Status | Date |
|----|-------|--------|------|
| ADR-000 | [Example: Use PostgreSQL over MySQL] | Accepted | [date] |

---

## Status Definitions

| Status | Meaning |
|--------|---------|
| Proposed | Under discussion, not yet decided |
| Accepted | Decision made and in effect |
| Rejected | Considered and explicitly rejected |
| Deprecated | Was accepted but no longer applies |
| Superseded | Replaced by a newer ADR (link provided) |

---

## How to Add an ADR

1. Copy `ADR-TEMPLATE.md`
2. Name it `ADR-[NNN].md` using the next sequential number
3. Fill in all sections
4. Add a row to the index table above
5. Set status to `Proposed` until the decision is confirmed
6. Update status to `Accepted` when confirmed with the user

ADR IDs are never reused. If a decision is reversed, write a new ADR that supersedes the old one.
