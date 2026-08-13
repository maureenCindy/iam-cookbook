# Security Policy

This repository holds **example applications** that demonstrate the
[IAM](https://iam.mpofusindie.dev) library. The recipes are teaching material —
they are intentionally small and are **not** hardened production deployments.

## Reporting a vulnerability

**Please do not open a public issue for a security problem.**

- **A flaw in a recipe here** (an example that teaches an unsafe pattern, leaks a
  secret, or misuses the library) — report it privately via this repository's
  **Security → Report a vulnerability** (GitHub private vulnerability reporting is
  enabled).
- **A vulnerability in the IAM library itself** (the `dev.mpofusindie:iam-*`
  artifacts or `@mpofusindie/iam-react`) — report it through the disclosure
  channel on the project site: <https://iam.mpofusindie.dev>. Do not file it
  against the examples repo.

Please include steps to reproduce, the affected recipe or artifact version, and
the impact you observed. You'll get an acknowledgement while it's triaged.

## Scope notes

- Recipes pin the **published** IAM artifacts
  (`dev.mpofusindie:iam-bom:2.0.0`, `@mpofusindie/iam-react@^1.4.0`); a
  vulnerability in a pinned dependency is tracked by Dependabot and addressed by
  bumping the recipe.
- Example credentials, seed users, and demo secrets committed in a recipe are
  **known and deliberate** for local runs — they are not a disclosure.
