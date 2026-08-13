# 08 · React guards tour

> Log in, guard a route, and show/hide UI by permission — the frontend half of IAM, wired to a live
> backend end-to-end.

**Stack:** Full-stack   **Status:** 🚧 not implemented yet

## The problem
Enforcement lives on the backend, but the UI still has to *reflect* it: don't route users to pages
they can't use, don't render buttons they can't click. Hard-coding that in the frontend drifts from
the real permissions instantly.

## The IAM solution
Wrap the app in `IAMProvider`, read decisions with `usePermissions`, gate routes with
`ProtectedRoute`, and show/hide features and actions with `FeatureGuard` / `ActionGuard` — all driven
by the same permissions the backend enforces. A small password-login helper covers sign-in before the
provider is mounted.

## Run it
_TBD — a two-role dashboard against the live backend: an admin sees the admin route and action
buttons, a viewer sees neither._

## The boundary this proves
The UI a user sees matches what the backend would allow — hidden routes/actions for the viewer,
visible for the admin — with the frontend never being the source of truth.

## Gotchas
- The guards are **UX**, not security — the backend is still the enforcer. Hiding a button is not
  protecting the endpoint (recipe 01 does that).
- `ProtectedRoute` integrates with your router; keep the peer dependency in mind.
