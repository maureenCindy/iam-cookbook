# 01 · Secure your first endpoint

> Put a permission check in front of a REST endpoint, log in to get a token, and watch the same
> request return `200` for an authorized user and `403` for everyone else.

**Stack:** Backend   **Status:** 🚧 not implemented yet

## The problem
You have a Spring Boot endpoint. You want "only users with permission X can call it" — without
standing up a policy server or writing a filter by hand.

## The IAM solution
One starter dependency, `@RequiresPermission("task", "read")` on the controller method, and a
boot-time seed that creates the resource, action, permission, and a user to hold it. Login returns
a JWT; the request carries it.

## Run it
_TBD — will end with two `curl`s against the same endpoint: one authorized (200), one not (403)._

## The boundary this proves
Authorized principal → `200`; authenticated-but-unpermitted principal → `403`; no token → `401`.

## Gotchas
- The difference between **authentication** (who are you) and **authorization** (what may you do) —
  a valid token is not a yes.
- Resources/actions must exist before a permission can reference them; the boot seed handles it.
