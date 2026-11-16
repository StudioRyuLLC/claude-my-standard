---
description: Guides the creation of new API endpoints. Use when adding routes, handlers, or controllers to the project.
---

# API Endpoint Conventions

Follow these conventions whenever you add or modify an API endpoint.

## Where Route Files Live

- Route files live in `src/routes/`, one file per resource (e.g. `src/routes/users.ts`).
- Handlers and controllers live in `src/controllers/`, one file per resource, mirroring the route file name.
- Request validation schemas live in `src/schemas/`, named after the resource.
- Register every new route file in `src/routes/index.ts`.

## Naming Conventions

- **Files:** kebab-case, singular or plural matching the resource (`user-profiles.ts`).
- **URL paths:** lowercase, kebab-case, plural nouns (`/api/v1/user-profiles`). Never use verbs in paths; the HTTP method carries the action.
- **Handler functions:** camelCase, verb first, then resource (`getUser`, `createUser`, `deleteUser`, `listUsers`).
- **HTTP methods:** `GET` read, `POST` create, `PUT`/`PATCH` update, `DELETE` remove.
- **Versioning:** all endpoints are prefixed with `/api/v1/`.

## Error Handling Pattern

- Wrap every async handler in the shared `asyncHandler` utility so rejected promises reach the error middleware. Do not write ad-hoc `try/catch` blocks that send responses.
- Throw typed errors (`NotFoundError`, `ValidationError`, `UnauthorizedError`, `ForbiddenError`) from handlers and services. A single error-handling middleware converts them to responses.
- Use correct status codes: `400` validation, `401` unauthenticated, `403` forbidden, `404` not found, `409` conflict, `500` unexpected.
- Never leak stack traces or internal error messages to clients. Log them server-side instead.

## Response Shape

All responses use a consistent JSON envelope.

Success:

```json
{
  "success": true,
  "data": { },
  "meta": { }
}
```

Error:

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Human-readable description",
    "details": [ ]
  }
}
```

- `meta` is optional and used for pagination (`page`, `pageSize`, `total`).
- `error.code` is an uppercase SNAKE_CASE constant.
- Use `201` for creation, `204` (no body) for deletion, `200` otherwise.

## What Must Be Present

Every new endpoint must have:

1. **Input validation** for params, query, and body using a schema in `src/schemas/`.
2. **Authentication and authorization** middleware, unless the endpoint is explicitly public (document why).
3. **The `asyncHandler` wrapper** and typed error handling as described above.
4. **The standard response envelope.**
5. **Tests** covering the success path, validation failure, and auth failure.
6. **Documentation**: an entry in the API docs (OpenAPI spec or equivalent) describing the path, method, request, and responses.
