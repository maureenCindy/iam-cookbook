# 05 · Multi-tenant SaaS

> Two tenants, one deployment: each request is routed to the right tenant, data stays isolated, and
> a brand-new tenant can be provisioned and seeded on the fly.

**Stack:** Backend   **Status:** 🚧 not implemented yet

## The problem
A SaaS app serves many customers from one running instance. Tenant A must never see tenant B's data,
requests have to be attributed to a tenant, and onboarding a new customer can't mean a redeploy.

## The IAM solution
Shared-schema tenant isolation with a tenant discriminator, pluggable **tenant resolution**
(subdomain, `X-Tenant-ID` header, or a JWT claim), and a **provisioning** call that creates a tenant
and seeds its baseline roles/permissions.

## Run it
_TBD — boot with two tenants on two subdomains; show a request under each seeing only its own data;
provision a third at runtime._

## The boundary this proves
A request resolved to tenant A → sees only A's data; the same credentials under B → only B's;
provisioning creates an isolated, immediately-usable tenant.

## Gotchas
- **Resolution must fail closed** — an unresolved tenant is a rejection, not a fallback to a default.
- Schema-per-tenant isolation is a separate, heavier recipe; this one does the common shared-schema
  case first.
