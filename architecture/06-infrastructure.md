# Category 6 — Infrastructure and Local Development

**Status:** Draft
**Last Updated:** [date]
**Maps to:** Arc42 Chapter 7

---

## Local Development

**Toolchain:** [Docker Compose / bare processes / devcontainer]

### Services and Ports

| Service | Port | Health check | Depends on |
|---------|------|-------------|------------|
| | | | |

### Startup Order

```
1. [service] — reason
2. [service] — reason
3. [service] — reason
```

### Environment Variables (local)

| Variable | Safe placeholder value | Description |
|----------|----------------------|-------------|
| DATABASE_URL | postgres://user:pass@localhost:5432/dbname | |
| | | |

---

## Production Hosting

**Target platform:** [AWS / GCP / Vercel / Railway / etc.]

**Differences from local:**

| Aspect | Local | Production |
|--------|-------|------------|
| Database | Docker container | Managed service |
| | | |

---

## Persistent Storage

| Volume / Bucket | Purpose | Backup strategy |
|----------------|---------|-----------------|
| | | |

---

## Container Strategy

[Docker images, base images, build strategy, image tagging]

---

## Deployment Diagram

```mermaid
graph TB
    subgraph Local["Local Development"]
        Compose["Docker Compose"]
        LocalDB[("PostgreSQL\n[Container]")]
        LocalAPI["API Server\n[Container]"]
        LocalFE["Frontend\n[Container]"]
    end

    subgraph Prod["Production"]
        CDN["CDN / Edge\n[e.g. Cloudflare]"]
        ProdFE["Frontend\n[e.g. Vercel]"]
        ProdAPI["API Server\n[e.g. Railway]"]
        ProdDB[("Managed DB\n[e.g. Supabase]")]
    end

    CDN --> ProdFE
    ProdFE -->|"REST"| ProdAPI
    ProdAPI -->|"SQL"| ProdDB

    style LocalDB fill:#2d6a4f,color:#fff
    style ProdDB fill:#2d6a4f,color:#fff
    style CDN fill:#6b6b6b,color:#fff
```

*Replace with actual services and platforms.*

---

## Notes and Clarifications

[Any context that does not fit above but is relevant to this category]
