<p align="center">
  <img src="./logo.png" alt="Idela logo" width="340"/>
</p>

<p align="center">
  <img src="https://readme-typing-svg.demolab.com/?font=Orbitron&weight=700&size=52&duration=1&pause=100000&repeat=false&color=0D1B2A&center=true&vCenter=true&width=500&height=80&lines=IDELA" alt="Idela"/>
</p>
<p align="center"><b>Idea → Architecture Design System</b></p>
<p align="center">A structured, Claude-driven process for turning a raw idea into a reviewed,<br/>decision-locked architecture package — before any feature spec or code gets written.</p>

<p align="center">
  <img src="https://img.shields.io/badge/stage-0%20%E2%80%94%20idea%20intake-lightgrey" alt="stage badge"/>
  <img src="https://img.shields.io/badge/license-proprietary%20%2B%20collaborative-black" alt="license badge"/>
</p>

---

This repository is not an application. It is a **workflow scaffold**: a set of
templates and a governing protocol (`CLAUDE.md`) that tells Claude Code exactly
how to behave in this project, stage by stage, session by session.

---

<details open>
<summary><img src="https://api.iconify.design/material-symbols:lightbulb-outline.svg?color=%23000000" width="20" height="20" align="absmiddle" alt="Why this exists icon"/> &nbsp;<b>Why This Exists</b></summary>

<br/>

Feature specs are implementation contracts. They only work when the structural
decisions behind them are already locked. Writing specs before the architecture
is designed produces specs that conflict with each other, invent constraints on
the fly, and miss dependencies that cause expensive refactors mid-build.

This system front-loads that effort. It combines documented practices from elite
engineering teams into one reusable process:

| Practice | Source | Contribution |
| --- | --- | --- |
| Working Backwards | Amazon | Define the customer outcome before the design |
| Design Docs | Google | Goals / Non-Goals / Alternatives structure |
| Arc42 | — | 12-category architecture documentation template |
| C4 Model | — | Four-level diagram vocabulary (System, Container, Component, Code) |
| MADR | — | Architecture Decision Record format |
| RFC Process | Rust / Ember / React | Draft → Review → Decision → Implementation lifecycle |

These aren't competing systems — they cover different layers of the same problem.
`ARCH_DESIGN_PROCESS.md` is the full specification of how they fit together.
`CLAUDE.md` is the operational protocol that makes Claude actually run it.

</details>

<details>
<summary><img src="https://api.iconify.design/material-symbols:settings-outline.svg?color=%23000000" width="20" height="20" align="absmiddle" alt="How it works icon"/> &nbsp;<b>How It Works</b></summary>

<br/>

Every session in this project, Claude:

1. Reads `STATUS.md` to know the current stage and what happened last session.
2. Reads `vision/VISION.md` and `decisions/DECISIONS.md` if they have content.
3. Scans `architecture/` for anything written beyond a template header.
4. Opens with a fixed status block (current stage, last session summary, what
   must happen this session) and asks: **"Ready to continue?"**

Claude acts as a **senior engineering manager and devil's advocate** throughout —
pressure-testing assumptions, naming risky decisions explicitly, and refusing to
move to the next stage until the current one is complete and you've explicitly
approved it. See `CLAUDE.md` for the full behavioral contract (what Claude must
always do, what it must never do).

</details>

<details>
<summary><img src="https://api.iconify.design/material-symbols:timeline.svg?color=%23000000" width="20" height="20" align="absmiddle" alt="Six stages icon"/> &nbsp;<b>The Six Stages</b></summary>

<br/>

```text
Stage 0 — Idea Intake
  No documents exist yet. Extract the problem, the user, and why now.
  Gate: you confirm a two-sentence summary of the idea.

Stage 1 — Vision Document (vision/VISION.md)
  Working Backwards: Customer & Problem, The Product, Goals, Non-Goals,
  Risks & Open Questions — filled in section by section through conversation.
  Gate: you explicitly approve VISION.md.

Stage 2 — Architecture Package (architecture/01–12)
  12 Arc42-mapped categories, one ADR per significant decision made along
  the way. Requires C4 diagrams (L1/L2 minimum) as Mermaid.
  Gate: you explicitly approve the full package.

Stage 3 — Architecture Review (review/REVIEW-LOG.md)
  Full pass read as an implementer, not the author: "what breaks if I build
  exactly what this says?" Findings logged by severity (Critical/High/Medium/Low).
  Gate: all Critical and High findings resolved or explicitly phase-assigned.

Stage 4 — Decisions Before Code (decisions/ADR-*.md, decisions/DECISIONS.md)
  Every implicit decision (repo structure, DB, auth, frontend, infra, etc.)
  surfaced and recorded as an ADR. No decision left as TBD.
  Gate: you explicitly approve the ADR log.

Stage 5 — Feature Specs (specs/F001.md, F002.md, ...)
  Specs derived only from the approved architecture package — no new
  architectural decisions get made at this stage. If a spec can't be
  completed from the architecture docs alone, that's a signal to go
  back to Stage 2, not to improvise.
```

Every stage has an explicit **gate**: Claude will not advance until you've given
clear approval. Nothing moves forward on momentum or enthusiasm alone.

</details>

<details>
<summary><img src="https://api.iconify.design/material-symbols:folder-outline.svg?color=%23000000" width="20" height="20" align="absmiddle" alt="Repository layout icon"/> &nbsp;<b>Repository Layout</b></summary>

<br/>

```text
.
├── CLAUDE.md                    Session protocol Claude follows every time (read first)
├── ARCH_DESIGN_PROCESS.md       Full specification of the 6-stage process
├── STATUS.md                    Current stage, last session summary, open questions
│
├── vision/
│   └── VISION.md                Stage 1 output — Working Backwards document
│
├── architecture/
│   ├── 01-context.md            Product vision & context (C4 L1)
│   ├── 02-overview.md           Architecture overview (C4 L2 — containers)
│   ├── 03-services.md           Service/module design (C4 L3 — components)
│   ├── 04-data-model.md         Tables, relationships, indexes, ER diagram
│   ├── 05-api-contracts.md      Every endpoint: method, auth, request/response, errors
│   ├── 06-infrastructure.md     Local dev, env vars, hosting, deployment diagram
│   ├── 07-security.md           AuthN/AuthZ model, audit events, compliance
│   ├── 08-quality.md            Latency/throughput/availability targets, a11y
│   ├── 09-build-order.md        Phase sequence, release gates, MVP done definition
│   ├── 10-testing.md            Unit/integration/e2e split, coverage targets
│   ├── 11-risks.md              Known risks, open ambiguities, reversibility
│   └── 12-glossary.md           Every domain term and acronym, defined once
│
├── decisions/
│   ├── DECISIONS.md             Append-only ADR index
│   ├── ADR-TEMPLATE.md          MADR-format template for new ADRs
│   └── ADR-*.md                 One file per accepted architecture decision
│
├── review/
│   └── REVIEW-LOG.md            Append-only log of every architecture review pass
│
└── specs/
    ├── SPEC-TEMPLATE.md         Feature spec template (Sources/Decisions/Constraints/...)
    └── F*.md                    One spec per MVP feature, derived from architecture + ADRs
```

</details>

<details>
<summary><img src="https://api.iconify.design/material-symbols:monitoring-outline.svg?color=%23000000" width="20" height="20" align="absmiddle" alt="Current status icon"/> &nbsp;<b>Current Status</b></summary>

<br/>

This instance of the system is freshly initialized and has not been run yet:

- **Stage:** 0 — Idea Intake
- **Vision, architecture, decisions, review, and specs:** all template-only, no content
- **Next step:** describe your idea to Claude in this project. It will run the
  Session Start Protocol, land on Stage 0, and ask for the problem, the user,
  and why now.

Check `STATUS.md` at any time for the authoritative current state.

</details>

<details>
<summary><img src="https://api.iconify.design/material-symbols:play-circle-outline.svg?color=%23000000" width="20" height="20" align="absmiddle" alt="Using this system icon"/> &nbsp;<b>Using This System</b></summary>

<br/>

1. Open a Claude Code session in this directory.
2. Claude reads `STATUS.md` and the other governing files, then opens with the
   stage status block automatically — you don't need to invoke anything.
3. Answer its questions plainly. Claude fills in the documents from your answers;
   you are never asked to write the templates yourself.
4. At the end of each stage, Claude will summarize what's done, what the next
   stage needs, and ask if you're ready to move on. Say so explicitly, or push
   back if something isn't right — pushing back is expected and welcome.
5. `STATUS.md` is updated at the end of every session so the next session can
   resume with full context.

</details>

<details>
<summary><img src="https://api.iconify.design/material-symbols:architecture-outline.svg?color=%23000000" width="20" height="20" align="absmiddle" alt="Design principles icon"/> &nbsp;<b>Design Principles Behind This System</b></summary>

<br/>

- **Documents are derived, not authored by the user.** You provide the raw
  input through conversation; Claude writes the structured output.
- **Nothing is TBD.** Every decision checklist item either gets a decision and
  an ADR, or is explicitly deferred to a named phase with a reason.
- **The architecture package is the source of truth.** If a later spec
  conflicts with an architecture document, the architecture document is fixed
  first, then the spec.
- **Non-goals are first-class.** An unnamed non-goal becomes an implicit goal
  that someone eventually argues for or is surprised isn't there.
- **Review is adversarial by design.** The review stage is read "as an
  implementer, not the author" specifically to surface the class of gaps that
  self-review misses.
- **All logs are append-only.** `DECISIONS.md` and `REVIEW-LOG.md` never have
  entries deleted — superseded decisions are superseded in writing, not erased.

For the full rationale, required questions per category, and failure modes this
process is designed to prevent, see `ARCH_DESIGN_PROCESS.md`.

</details>

<details>
<summary><img src="https://api.iconify.design/material-symbols:gavel-outline.svg?color=%23000000" width="20" height="20" align="absmiddle" alt="License icon"/> &nbsp;<b>License</b></summary>

<br/>

© 2026 Alexza (Allexzaa). All rights reserved.

This is proprietary work, not open-source. No copy, duplicate, redistribution,
or derivative publication is permitted without the author's prior written
permission. Improvements and contributions are welcome — you're encouraged to
share fixes and extensions back with the author, though doing so does not
transfer ownership or grant redistribution rights.

See [`LICENSE`](./LICENSE) for the full terms.

</details>
