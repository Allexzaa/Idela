# Architecture-First Design Process

A universal pre-build system for non-trivial software projects.
Run every stage in this document before writing a feature spec or any code.

---

## What This Is

This process combines the documented practices of elite engineering teams into a
single reusable system:

- **Google** — Design Docs: written before coding, Goals/Non-Goals, Alternatives
- **Amazon** — Working Backwards: define the customer outcome before the design
- **Rust / Ember / React** — RFC lifecycle: Draft → Review → Decision → Implementation
- **MADR standard** — Architecture Decision Records: one decision per record, append-only
- **Arc42** — Architecture documentation template: 12 structured categories
- **C4 Model** — Four levels of architecture diagrams: System, Container, Component, Code

These are not competing systems. They address different layers of the same problem.
This document tells you how to use them together.

---

## Why Architecture First

Feature specs are implementation contracts. They only work when the structural decisions
behind them are already locked. Writing specs before designing the architecture produces
specs that conflict each other, invent constraints, and miss dependencies that cause
expensive refactors mid-build.

The cost is front-loaded effort. The return is a build phase without structural surprises.

---

## The Process at a Glance

```text
Stage 1 — Vision
  Write the Working Backwards document.
  Define the customer outcome before defining the product.

Stage 2 — Architecture Package
  Write the full system design across all required categories.
  Output: a version-controlled folder of architecture documents.

Stage 3 — Architecture Decision Records
  Write one ADR per significant decision as it is made during Stage 2.
  Output: an ADR log that becomes the project's DECISIONS.md.

Stage 4 — Architecture Review
  Run at least one review pass using the RFC severity protocol.
  Resolve all Critical and High findings before Stage 5.

Stage 5 — Decisions Before Code
  Lock all structural decisions that would cause refactors if left ambiguous.
  Output: confirmed ADR entries and an approved build order.

Stage 6 — Feature Specs
  Derive specs from architecture documents, not from scratch.
  Each spec references the architecture docs that justify it.
```

---

## Stage 1 — Vision Document (Working Backwards)

Originating from Amazon's product development process. Write this before any
technical design begins. If you cannot write it clearly, the project is not
ready to design.

### Required Sections

**Customer and Problem**

- Who is the target user, in what context, doing what specific task?
- What is the painful or broken experience today?
- What does success look like from the user's point of view?

**The Product**

- One paragraph describing what the product is and what it is not.
- The core customer promise in one sentence.
- Two to three concrete user workflow examples (not abstract personas).

**Goals**

- What the product must achieve at MVP.
- What success looks like in measurable terms.

**Non-Goals**

Non-goals are not negated goals ("won't crash"). They are things that could
reasonably be goals, but are explicitly chosen not to be. Name them and say why.

**Risks and Open Questions**

- What assumptions could be wrong?
- What would kill the product if discovered late?
- What must be validated before significant build effort begins?

### Done Criteria

- [ ] A developer who has not seen the project can read this document and describe
  the product accurately in their own words.
- [ ] All non-goals are named and explained.
- [ ] At least one user workflow is concrete enough to trace through the system end-to-end.

---

## Stage 2 — Architecture Package

Write one document per category below. Depth scales with complexity. A simple service
may cover multiple categories in one file. A complex system may need multiple files per
category. Arc42 provides the structural framework; C4 provides the diagram vocabulary.

### C4 Diagram Levels (use across all documents)

| Level       | What it shows                                        | When to use                    |
|-------------|------------------------------------------------------|--------------------------------|
| L1 System   | Your system in relation to users and external systems | Always — first diagram to draw |
| L2 Container | Apps, services, databases, message brokers           | Always — shows deployable units |
| L3 Component | Internal structure of one container                  | When a service is complex enough |
| L4 Code     | Classes, functions, modules                          | Rarely — code is usually enough |

Text-based diagrams (ASCII or Mermaid) are acceptable. Diagrams do not need
to be formal UML.

---

### Category 1 — Product Vision and Context

Maps to: Arc42 Chapter 1 (Introduction and Goals) and C4 Level 1 (System Context).

Must answer:

- What problem does this system solve?
- Who are the users and external systems?
- What are the top 3–5 quality goals (non-functional requirements) that drive architectural decisions?
- What constraints exist (legal, technical, organizational) that the architecture must not violate?

---

### Category 2 — Architecture Overview

Maps to: Arc42 Chapter 4 (Solution Strategy) and C4 Level 2 (Container Diagram).

Must answer:

- What is the top-level data flow from input to output?
- What are the deployable units (containers) and what does each own?
- What does each container explicitly NOT own? (naming boundary violations is as
  important as naming responsibilities)
- What is the data ownership principle? (which layer is the single source of truth for what)
- Why does this architecture work? (what failure modes does it prevent)

---

### Category 3 — Service and Module Design

Maps to: Arc42 Chapter 5 (Building Block View) and C4 Level 3 (Component Diagram).

Must answer:

- What are the internal modules or domains of each service?
- How do services communicate? (REST, events, queues, gRPC — and why)
- What are the shared contracts between services? (schemas, event types, enums)
- Who can import from whom? (dependency direction rules)
- What pattern governs dependency injection or service instantiation?

---

### Category 4 — Data Model

Maps to: Arc42 Chapter 9 (Architecture Decisions — data).

Must answer:

- What are all tables or collections with their fields and types?
- What are the relationships, foreign keys, and cascade rules?
- What indexes exist, and why? (include non-obvious ones)
- What are the known scaling limitations of this model?
- What enums exist and what are their allowed values?
- What is explicitly NOT in the data model at this stage and why?

---

### Category 5 — API Contracts

All endpoints the system exposes, at a level where implementation can begin
without any ambiguity.

Must answer:

- Method, path, authentication requirement, request body, response shape for every endpoint.
- Error response format and error codes.
- Rate limiting rules per endpoint.
- What is NOT in the API at this stage?

---

### Category 6 — Infrastructure and Local Development

Maps to: Arc42 Chapter 7 (Deployment View).

Must answer:

- How does the system run locally? (Docker Compose, services, ports, health checks, startup order)
- What environment variables exist, with safe placeholder values?
- What is the production hosting target and what differs from local?
- What are the named volumes or persistent storage requirements?
- What is the container or process strategy?

---

### Category 7 — Security and Access Control

Maps to: Arc42 Chapter 8 (Cross-cutting Concepts — security).

Must answer:

- What is the authentication strategy? (provider, token type, storage location)
- What is the authorization model? (role-based, attribute-based, ACL)
- Where is authorization enforced? (at what layer)
- What does a misconfiguration leak?
- What audit events must be captured and when?
- What compliance constraints affect the build?

---

### Category 8 — Quality Requirements and Non-Functional Constraints

Maps to: Arc42 Chapter 10 (Quality Requirements).

Must answer:

- What are the latency, throughput, and availability targets?
- What are the scalability constraints at MVP vs. production?
- What is the data retention or privacy requirement?
- What browser, device, or platform support is required?
- What accessibility standard applies?

---

### Category 9 — Build Order and Release Gates

Must answer:

- What is the complete build sequence with one-line descriptions per phase?
- Why is this order correct? (what does each phase unlock for the next)
- What is the first critical milestone? (minimum to prove the backbone works)
- What release gates define "done" at each major milestone?
- What is the full MVP done definition?

The build order determines feature IDs (F001, F002, ...) and the source of
all feature spec content.

---

### Category 10 — Testing Strategy

Maps to: Arc42 Chapter 8 (Cross-cutting Concepts — testing).

Must answer:

- What is the unit / integration / end-to-end split?
- What gets automated vs. manually verified?
- What are the required test coverage targets by component type?
- What must pass before each release gate?

---

### Category 11 — Known Risks and Open Ambiguities

Maps to: Arc42 Chapter 11 (Risks and Technical Debt).

Must answer:

- What assumptions could be wrong and what happens if they are?
- What technical choices are reversible vs. locked in?
- What is deferred and to which specific phase?
- What would cause a structural refactor if discovered after Phase 03?

---

### Category 12 — Glossary

Maps to: Arc42 Chapter 12 (Glossary).

Must include: every domain term, service name, and acronym used across the
architecture documents, with a one-line definition. Consistent terminology is a
non-negotiable baseline for any team larger than one person.

---

### Architecture Package Done Criteria

- [ ] All 12 categories have at least one document covering the required questions.
- [ ] Every service boundary has an explicit "must not own" list.
- [ ] A C4 Level 1 and Level 2 diagram exist.
- [ ] The data model covers all entities needed by the MVP build order.
- [ ] The build order is final with release gates and a done definition.
- [ ] All open ambiguities are listed in Category 11.

---

## Stage 3 — Architecture Decision Records (ADRs)

Write one ADR per significant decision as it arises during Stage 2. ADRs become the
project's DECISIONS.md and the source of truth for why the system is built the way it is.

This system uses the MADR format (Markdown Architectural Decision Records), which is the
most widely adopted standard. It is a superset of the original Nygard format.

### ADR Template

```markdown
# ADR-[NNN] — [Decision phrased as "Use X for Y" or "Choose X over Y"]

Date: [YYYY-MM-DD]
Status: Proposed | Accepted | Rejected | Deprecated | Superseded by ADR-[NNN]
Deciders: [who made this decision]

## Context and Problem Statement

[What situation made this decision necessary?
What forces are at play? What constraint or requirement triggered this?]

## Decision Drivers

- [The primary criterion any solution must satisfy]
- [Secondary criterion]
- [Hard constraint that eliminates options]

## Considered Options

- Option A: [name]
- Option B: [name]
- Option C: [name]

## Decision

Chosen option: **[Option X]**

[One paragraph explaining why this option best satisfies the decision drivers.]

## Consequences

Positive:

- [What this decision enables or makes easier]

Negative:

- [What this decision forecloses or makes harder]
- [What must be true for this decision to remain valid]

## Do Not Reverse Without

[What would have to change in the project for this decision to be revisited]

## Confirmation

[How will the team know this decision was correctly implemented?
What test, review, or observable behavior confirms it?]
```

### ADR Rules

- One decision per ADR. Never combine multiple decisions.
- Append-only. Superseded ADRs are never deleted — write a new ADR that supersedes.
- Status must be updated when a decision changes.
- The title must be a decision statement, not a topic ("Use PostgreSQL over MySQL" not "Database choice").
- ADRs are numbered sequentially and IDs are never reused.

---

## Stage 4 — Architecture Review (RFC Protocol)

Run at least one review pass after the architecture package is drafted.
Complex systems warrant multiple passes.

### Review Lifecycle

```text
Draft → Author Review → Peer Review → Final Comment Period → Decision → Resolved
```

- **Draft** — Architecture documents written but not yet reviewed.
- **Author Review** — Author reads every document as an implementer, not as the author. Ask: "What breaks if I build exactly what this says?"
- **Peer Review** — At least one other person (or Claude with the `/review-doc` command) reads each document. Comments submitted as structured findings.
- **Final Comment Period** — All findings are catalogued. Author produces a resolution table. No new findings after this point.
- **Decision** — Each finding is Accept, Modify, Reject, or Defer with full reasoning.
- **Resolved** — Changes applied. Resolution log appended to the architecture package.

### Finding Severity

| Severity    | Meaning                                                       | Must resolve before         |
|-------------|---------------------------------------------------------------|-----------------------------|
| Critical    | Structural refactor if missed — affects every subsequent phase | Any spec is written          |
| High        | Phase-level rework if missed                                  | The affected phase begins    |
| Medium      | Implementation rework or technical debt                       | The affected phase begins    |
| Low         | Clarification or quality improvement, no implementation risk  | Can defer to implementation  |

### What to Look For in a Review

- Boundary violations (a service doing what it must not own)
- Missing tables, fields, or indexes that a later phase will need
- Ambiguous ownership (two services could both claim a responsibility)
- Deferred items with no assigned phase (will be forgotten)
- Undocumented scaling limitations
- Security gaps requiring a refactor if caught late
- Phase-order violations (phase N depends on something built in phase N+2)
- Decisions with no documented reasoning (will be relitigated during build)
- Non-goals that are actually required (stated as out of scope but will be demanded)

### Resolution Log Format

Append to a dedicated file in the architecture package. One section per review pass.

```markdown
## Review Pass [N] — [YYYY-MM-DD]

### [SEVERITY]-[NNN] — [Short title]

Status: resolved | deferred to [phase] | rejected

Decision:
[What was decided and why]

Changes:
- [File name] — [what changed]
- [File name] — [what changed]
```

### Review Done Criteria

- [ ] All Critical findings resolved.
- [ ] All High findings resolved or assigned to a specific phase with a documented reason.
- [ ] Resolution log appended to the architecture package.
- [ ] Build order updated to reflect any changes discovered in review.

---

## Stage 5 — Decisions Before Code

After review, run a final lock-in pass. The purpose is to surface any decision
that was implicit in the architecture documents and make it explicit in the ADR log.
Ambiguous decisions become inconsistent implementations. Lock them now.

### Decision Checklist

Work through each category. Every item needs a decision and a recorded ADR entry.

**Repository Structure**

- [ ] Monorepo or multi-repo? Reasoning?
- [ ] Directory structure finalized and documented?
- [ ] Import and dependency rules defined?

**Service Boundaries**

- [ ] Every service boundary has an explicit "must not own" list?
- [ ] Inter-service communication contracts are defined?
- [ ] Shared packages and their consumers are named?

**Database**

- [ ] Database engine confirmed?
- [ ] ORM or query builder confirmed?
- [ ] Migration toolchain confirmed?
- [ ] Isolation model confirmed (row-level, schema, separate DB)?

**Authentication and Authorization**

- [ ] Auth provider or custom implementation?
- [ ] Token type, storage location, and refresh strategy?
- [ ] Authorization enforcement layer?

**Frontend**

- [ ] Framework confirmed?
- [ ] Server state vs. client state split defined?
- [ ] API client pattern confirmed?
- [ ] Design token system confirmed?

**Infrastructure**

- [ ] Local development toolchain confirmed?
- [ ] Production hosting target confirmed?
- [ ] Container strategy confirmed?

**AI / ML (if applicable)**

- [ ] Model provider for MVP confirmed?
- [ ] Mock-first or real-provider-first strategy?
- [ ] Evaluation strategy for model output quality?

**External Integrations (if applicable)**

- [ ] Which integration is built first and why?
- [ ] API-first, file-system, or event-based ingestion strategy?

### Stage 5 Done Criteria

- [ ] Every item above has a corresponding ADR entry.
- [ ] No decision is left as TBD.
- [ ] Every ADR entry has a rejected alternative and a reason.
- [ ] Build order is confirmed as the final sequence.

---

## Stage 6 — Deriving Feature Specs from Architecture

Feature specs are derived from the architecture package. They extract and formalize
what the architecture already decided. They do not make new architectural decisions.

### The Derivation Mapping

| Feature spec section  | Derived from                                        |
|-----------------------|-----------------------------------------------------|
| Sources               | Which architecture documents cover this phase       |
| Decisions             | Which ADR entries constrain this phase              |
| Constraints           | What the build order says this phase must NOT include |
| Deferred Items        | What the build order assigns to later phases        |
| Acceptance Criteria   | The release gate for this phase from Category 9     |
| What Comes Next       | The next phase entry in the build order             |

### How to Write a Spec from Architecture Documents

1. Open the build order. Find the phase matching this feature ID.
2. Open the architecture documents listed for that phase.
3. Set `Sources:` in the spec header to those documents.
4. Set `Decisions:` to the ADR IDs that constrain this phase.
5. Write the `Constraints` section from the build order's "not in this phase" notes.
6. Write the `Deferred Items` table from the build order's "next phase" entries.
7. Write `Acceptance Criteria` from the matching release gate in Category 9.
8. Write `What Comes Next` from the next phase entry in the build order.

If you cannot complete steps 3–8 from the architecture package alone, the architecture
package is not complete. Do not guess. Return to Stage 2.

### How to Derive ARCH Memory Files

After Stages 2–5 are complete:

- `ARCH-backend.md` is a condensed summary of Categories 2, 3, 4, 5, 6, and 7.
- `ARCH-frontend.md` is a condensed summary of the frontend portions of Categories 2, 3, and 5.

Write the `## Summary` section (5 lines max) last — it is the session-start snapshot.
The full files are the working reference. The summary is the session-optimized view.

---

## Ready Checklist — Before Writing F001

All items must be true before the first feature spec is written.

**Architecture Package**

- [ ] All 12 categories have at least one document.
- [ ] Every service boundary has an explicit "must not own" list.
- [ ] C4 Level 1 and Level 2 diagrams exist.
- [ ] Data model covers all MVP entities.
- [ ] Build order is final with release gates.

**Review**

- [ ] At least one review pass completed with a resolution log.
- [ ] All Critical findings resolved.
- [ ] All High findings resolved or phase-assigned with reasoning.

**ADRs**

- [ ] Every significant structural decision has an ADR entry.
- [ ] Every ADR has a rejected alternative and a reason.
- [ ] No decision is left as TBD.

**Memory Files**

- [ ] `ARCH-backend.md` populated from architecture documents.
- [ ] `ARCH-frontend.md` populated from architecture documents.
- [ ] `CLAUDE.md` filled in with stack, current direction, constraints.

**Ready Signal**

Answer these three questions without opening any spec file:

- What does Phase 02 depend on from Phase 01?
- What is explicitly deferred from Phase 01?
- What are the acceptance criteria for Phase 01?

If all three answers are immediate, the architecture is ready. If any require
guessing, return to Stage 2 and fill the gap.

---

## Common Failure Modes

**Starting specs before the architecture is complete.**
The spec will make architectural decisions by default. Those decisions will conflict
with decisions made in later specs. You will discover this during Phase 06.

**Writing ambiguities down without resolving them.**
An unresolved ambiguity in the architecture becomes an inconsistent implementation.
Either resolve it or explicitly defer it to a named phase with a plan.

**Skipping the review pass.**
Self-reviewed architecture misses the class of bugs visible only when reading
the document as an implementer. Read it cold. Ask: what breaks if I build exactly this?

**Making architecture documents too abstract.**
Documents without concrete table schemas, actual endpoint paths, and real environment
variable names are vision documents, not architecture documents. Vision documents
cannot be used to write specs.

**Making architecture documents too detailed.**
Line-level implementation detail belongs in code, not architecture docs. Architecture
documents describe structure and decisions. They do not prescribe implementation.

**Treating the architecture package as permanent.**
When a spec review finds an architecture gap, update the architecture document first.
The architecture package is the source of truth. Specs are derived from it.

**Skipping Non-Goals.**
A missing non-goal becomes an implicit goal. Someone will build it, or argue that
it should be built, or be surprised that it was not built. Name every reasonable
thing that is explicitly not in scope and say why.

---

## Reference: Standards Used in This System

| Standard       | What it contributes                                          |
|----------------|--------------------------------------------------------------|
| Amazon PR/FAQ  | Vision layer — customer outcome before technical design      |
| Google Design Doc | Goals/Non-Goals structure, Alternatives section           |
| Arc42          | 12-category architecture documentation template              |
| C4 Model       | Four-level diagram vocabulary (System, Container, Component) |
| MADR           | Architecture Decision Record format                          |
| RFC Process    | Review lifecycle: Draft → Review → Decision → Implementation |
