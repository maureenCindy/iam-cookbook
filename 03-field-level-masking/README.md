# 03 · Field-level masking

> The HR lead sees `salary` and `ssn`; a teammate gets `***` for the same record over the same
> endpoint — and the React table masks **exactly** what the API masked.

**Stack:** Full-stack   **Status:** 🚧 not implemented yet

## The problem
Row-level access isn't enough. Two users can be allowed to read the *same* employee record but must
see *different fields*. Doing this by hand means bespoke DTOs per role and drift between what the API
returns and what the UI shows.

## The IAM solution
Mark fields with `@FieldFiltered` / declare them `sensitive`, grant `visible` (read) and `editable`
(update) per field, and IAM masks the response by the caller's field grants. Masking is
**type-aware** — only the resource's own DTO is filtered, nested types aren't over-redacted. On the
frontend, `FieldGuard` reads the same decisions so the UI and payload never disagree.

## Run it
_TBD — one employee, two logins; `curl` shows the salary present vs masked, and the `web/` table
shows the matching UI state._

## The boundary this proves
Field-granted user → real value; ungranted user → masked, over the same endpoint and DTO; a field
declared `sensitive` with **no** grant → masked (default-deny, never leaks).

## Gotchas
- **`sensitive: true` is default-deny** — declaring a field sensitive and forgetting to grant it
  means it's hidden, not shown. That's the safe direction.
- `visible` governs reads, `editable` governs updates — a user can see a field they can't change.
- Non-nullable fields that get masked still have to satisfy the contract — mind the DTO shape.
