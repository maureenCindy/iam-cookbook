# 02 · Roles, groups, and deny-takes-precedence

> A user inherits "edit" through a **group**, but an explicit **deny** on one page overrides it —
> and the `explain` API tells you exactly why.

**Stack:** Backend   **Status:** 🚧 not implemented yet

## The problem
Real orgs don't assign permissions user-by-user. People are in groups, groups carry roles, and
sometimes you need to *revoke* one thing for one person without unwinding their whole role.

## The IAM solution
Group membership → role → permissions (inheritance). Then a user-level **DENY** that beats the
inherited grant, because IAM resolves **deny-takes-precedence**. The `explain` endpoint returns the
decision *and its reasons*, so "why can't I edit this?" is answerable.

## Run it
_TBD — seed an `editors` group with edit rights, add a per-user deny on one page, show the allow on
other pages and the deny on that one._

## The boundary this proves
Group member → can edit pages in general; the explicitly-denied page → refused even for that same
member; `explain` names the deny as the deciding rule.

## Gotchas
- **Deny always wins** — a later, more specific grant does *not* re-open a deny. This is the safe
  default and a classic system-design talking point.
- Inheritance is through the group's role, not copied onto the user — removing them from the group
  removes the access.
