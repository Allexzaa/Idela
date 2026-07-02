# Category 5 — API Contracts

**Status:** Draft
**Last Updated:** [date]

---

## Authentication

**Type:** [Bearer token / API key / Session cookie]
**Header:** `Authorization: Bearer <token>`
**How to obtain a token:** [endpoint or flow]

---

## Error Response Format

All errors follow this shape:

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable description",
    "details": {}
  }
}
```

| HTTP Status | When used |
|-------------|-----------|
| 400 | Validation error |
| 401 | Missing or invalid token |
| 403 | Authenticated but not authorized |
| 404 | Resource not found |
| 409 | Conflict (duplicate, state violation) |
| 422 | Business logic rejection |
| 429 | Rate limit exceeded |
| 500 | Internal server error |

---

## Rate Limiting

| Tier | Limit | Window | Applies to |
|------|-------|--------|------------|
| Default | | per minute | All endpoints |
| | | | |

---

## Endpoints

One section per endpoint group.

---

### [Resource Name]

#### `POST /api/v1/[resource]`

**Auth required:** Yes / No
**Description:** [What this does in one line]

**Request body:**
```json
{
  "field": "type — description"
}
```

**Response `201`:**
```json
{
  "id": "uuid",
  "field": "value"
}
```

**Errors:**
| Code | When |
|------|------|
| 400 | |
| 409 | |

---

#### `GET /api/v1/[resource]/:id`

**Auth required:** Yes / No
**Description:** [What this does in one line]

**Response `200`:**
```json
{
  "id": "uuid",
  "field": "value"
}
```

**Errors:**
| Code | When |
|------|------|
| 404 | Resource not found |

---

## What is NOT in the API at This Stage

| Excluded endpoint | Reason | Deferred to |
|------------------|--------|-------------|
| | | Phase [N] |

---

## Notes and Clarifications

[Any context that does not fit above but is relevant to this category]
