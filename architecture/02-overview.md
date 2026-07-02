# Category 2 — Architecture Overview

**Status:** Draft
**Last Updated:** [date]
**Maps to:** Arc42 Chapter 4 + C4 Level 2

---

## Top-Level Data Flow

[What is the data flow from input to output? Walk through the system step by step.]

```
Input → [step] → [step] → [step] → Output
```

---

## Deployable Units (Containers)

Each row is a container — an independently deployable unit.

| Container | Technology | Owns | Must NOT own |
|-----------|------------|------|--------------|
| | | | |

---

## Data Ownership

Which layer is the single source of truth for what.

| Data domain | Owner container | Other containers may |
|-------------|----------------|----------------------|
| | | Read only / No access |

---

## Why This Architecture Works

[What failure modes does this architecture prevent? What would break if the boundaries were different?]

---

## L2 Container Diagram

```mermaid
graph TB
    User["User\n[Person]"] -->|"HTTPS"| Frontend["Frontend App\n[Container: React]"]
    Frontend -->|"REST / HTTPS"| API["API Server\n[Container: Node.js]"]
    API -->|"SQL"| DB[("Database\n[Container: PostgreSQL]")]
    API -->|"HTTPS"| Ext["External Service\n[External System]"]

    style User fill:#08427b,color:#fff
    style Frontend fill:#1168bd,color:#fff
    style API fill:#1168bd,color:#fff
    style DB fill:#2d6a4f,color:#fff
    style Ext fill:#6b6b6b,color:#fff
```

*Replace placeholder names, technologies, and connections with the actual system design.*

---

## Notes and Clarifications

[Any context that does not fit above but is relevant to this category]
