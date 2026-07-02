# Architecture Review Log

All review passes are recorded here. One section per pass.
This file is append-only — never delete previous review passes.

---

## Review Status

**Total passes completed:** 0
**All Critical findings resolved:** —
**All High findings resolved or phase-assigned:** —
**Ready to proceed to Stage 4:** No

---

## Finding Severity Reference

| Severity | Meaning | Must resolve before |
|----------|---------|---------------------|
| Critical | Structural refactor if missed — affects every subsequent phase | Any spec is written |
| High | Phase-level rework if missed | The affected phase begins |
| Medium | Implementation rework or technical debt | The affected phase begins |
| Low | Clarification or quality improvement, no implementation risk | Can defer to implementation |

---

## Review Pass Template

Copy this section for each review pass.

```
## Review Pass [N] — [YYYY-MM-DD]

Reviewer: [name or "Claude — architect review"]
Scope: [which documents were reviewed]

### Summary

[N] Critical findings
[N] High findings
[N] Medium findings
[N] Low findings

### Findings

#### CRITICAL-001 — [Short title]

Status: Open | Resolved | Deferred to Phase [N]

Finding:
[What the problem is. Be specific about which document and which section.]

Impact:
[What breaks during build if this is not resolved before coding begins.]

Decision:
[What was decided and why. Who decided it.]

Changes:
- [file name] — [what changed]

---

#### HIGH-001 — [Short title]

Status: Open | Resolved | Deferred to Phase [N]

Finding:
[...]

Impact:
[...]

Decision:
[...]

Changes:
- [file name] — [what changed]
```

---

## Review Checklist

Use this during each review pass.

- [ ] Boundary violations (a service doing what it must not own)
- [ ] Missing tables, fields, or indexes that a later phase will need
- [ ] Ambiguous ownership (two services could both claim a responsibility)
- [ ] Deferred items with no assigned phase (will be forgotten)
- [ ] Undocumented scaling limitations
- [ ] Security gaps requiring a refactor if caught late
- [ ] Phase-order violations (phase N depends on something built in phase N+2)
- [ ] Decisions with no documented reasoning (will be relitigated during build)
- [ ] Non-goals that are actually required (stated as out of scope but will be demanded)
- [ ] Mermaid diagrams match the text in their respective documents
