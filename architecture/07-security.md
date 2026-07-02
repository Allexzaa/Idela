# Category 7 — Security and Access Control

**Status:** Draft
**Last Updated:** [date]
**Maps to:** Arc42 Chapter 8 (security)

---

## Authentication Strategy

| Aspect | Decision |
|--------|----------|
| Provider | [Auth0 / Clerk / Supabase Auth / custom / etc.] |
| Token type | [JWT / opaque token / session cookie] |
| Token storage | [httpOnly cookie / memory / localStorage — explain why] |
| Token expiry | |
| Refresh strategy | |

---

## Authorization Model

**Model type:** [Role-based (RBAC) / Attribute-based (ABAC) / ACL]

### Roles

| Role | Description | Permissions |
|------|-------------|-------------|
| | | |

### What a misconfiguration leaks

[If the auth layer is misconfigured or bypassed, what data or actions become accessible?]

---

## Where Authorization is Enforced

| Layer | What it enforces | What it does NOT enforce |
|-------|-----------------|--------------------------|
| API middleware | | |
| Service layer | | |
| Database (RLS) | | |

Authorization must not be enforced only at the UI layer.

---

## Audit Events

| Event | When it is captured | What is logged |
|-------|--------------------|--------------  |
| | | |

---

## Compliance Constraints

| Constraint | Source | Architectural impact |
|------------|--------|----------------------|
| | GDPR / HIPAA / SOC2 / etc. | |

---

## Notes and Clarifications

[Any context that does not fit above but is relevant to this category]
