# Category 10 — Testing Strategy

**Status:** Draft
**Last Updated:** [date]
**Maps to:** Arc42 Chapter 8 (testing)

---

## Test Split

| Type | Scope | Tooling | Automated |
|------|-------|---------|-----------|
| Unit | Pure functions, business logic | | Yes |
| Integration | Service + database, service + external | | Yes |
| End-to-end | Full user flows | | Yes / Manual |
| Manual | Exploratory, edge cases, UX | — | No |

---

## Coverage Targets by Component

| Component | Target coverage | Rationale |
|-----------|----------------|-----------|
| Business logic / domain | % | High risk, pure functions — easy to test |
| API handlers | % | |
| Data access layer | % | |
| Frontend components | % | |
| End-to-end flows | [N] critical paths | |

---

## What Gets Automated vs. Manually Verified

**Automated:**
-
-

**Manually verified before each release gate:**
-
-

---

## Release Gate Requirements

| Gate | Must pass before |
|------|-----------------|
| Phase 01 complete | |
| Phase 02 complete | |
| MVP release | |

---

## Notes and Clarifications

[Any context that does not fit above but is relevant to this category]
