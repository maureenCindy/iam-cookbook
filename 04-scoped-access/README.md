# 04 · Scoped access (the RBAC → ABAC bridge)

> A doctor with the `ward-clinician` role can act **only within their own ward** — same role, same
> permissions, bounded by scope.

**Stack:** Backend   **Status:** 🚧 not implemented yet

## The problem
"Clinician" isn't one flat capability. Every clinician has the same *kind* of access but over a
*different slice* of the data. Plain RBAC would need a role per ward; that doesn't scale.

## The IAM solution
Scoped role assignments: the same role is granted **within a scope**, and `scopeParam` binds the
request's target (e.g. the ward id) to the caller's granted scope. This is the bridge from RBAC
toward ABAC without a policy language.

## Run it
_TBD — two clinicians in two wards; each succeeds inside their ward and is refused in the other._

## The boundary this proves
Clinician acting inside their granted scope → allowed; the *same* clinician against another ward →
refused; a missing `scopeParam` does **not** silently widen to tenant-wide.

## Gotchas
- **A scope is a grant boundary, not a row filter.** IAM proves *your role is in scope*; returning
  only in-scope *rows* is still your query's job. Conflating the two is the #1 misread.
- If `scopeParam` can't resolve the parameter, that's a fail-fast at boot, not a silent widen.
