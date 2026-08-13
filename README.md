# IAM Cookbook

Runnable recipes for [**IAM**](https://iam.mpofusindie.dev) — embedded authorization for
Spring Boot. Each recipe is a small, self-contained app that solves **one** real access-control
problem, with a README that frames the problem, the IAM solution, and the gotchas — and a test
that proves the allow/deny boundary.

Every recipe consumes the **published** artifacts, exactly as a real adopter would:

> **Maven**: `dev.mpofusindie:iam-bom:2.0.0` · **npm**: `@mpofusindie/iam-react@^1.4.0`

No `mavenLocal`, no vendored tarballs — if a recipe runs, your app will too.

---

## Start here — what makes IAM different

Most access-control libraries stop at "which endpoints can this role call?". These three recipes
show the parts that don't:

| Recipe | The thing you can't easily do elsewhere |
|--------|------------------------------------------|
| [03 · Field-level masking](03-field-level-masking/) | Hide `salary`/`ssn` on a *per-field* basis — and have the **React UI mask exactly what the API masks** |
| [04 · Scoped access](04-scoped-access/) | "This doctor sees only *their* ward" — role-in-scope, the RBAC→ABAC bridge |
| [05 · Multi-tenant SaaS](05-multi-tenant-saas/) | Tenant isolation, resolution (subdomain/header/JWT), and provisioning a new tenant |

## The full index

Read top-to-bottom and it tells a story: hook → real RBAC → the differentiators → *can I adopt
it?* → *is it production-ready?* → the React side.

| # | Recipe | What it teaches | Stack |
|---|--------|-----------------|-------|
| 01 | [secure-first-endpoint](01-secure-first-endpoint/) | `@RequiresPermission`, boot-seed, login → token. The 5-minute front door. | Backend |
| 02 | [roles-groups-and-deny](02-roles-groups-and-deny/) | Roles vs **groups** (inheritance), **deny-takes-precedence**, the `explain` API | Backend |
| 03 | [field-level-masking](03-field-level-masking/) | `@FieldFiltered`, `sensitive` = default-deny, `visible` vs `editable`, type-aware masking | Full-stack |
| 04 | [scoped-access](04-scoped-access/) | Scoped roles, `scopeParam`, "a scope is a grant boundary, not a row filter" | Backend |
| 05 | [multi-tenant-saas](05-multi-tenant-saas/) | Tenant isolation, resolution strategies, tenant provisioning | Backend |
| 06 | [add-iam-to-existing-app](06-add-iam-to-existing-app/) | Drop the starter into an app that already has JPA + Flyway, without breaking it; the contract-only `iam-api` module | Backend |
| 07 | [audit-and-observability](07-audit-and-observability/) | Stream audit events to your own ledger (`IamAuditSink`); Micrometer metrics | Backend |
| 08 | [react-guards-tour](08-react-guards-tour/) | `IAMProvider`, `usePermissions`, `ProtectedRoute`, `FeatureGuard`/`ActionGuard`, password login | Full-stack |

> **Status:** the repo is scaffolded; recipes are being filled in one at a time. A recipe's
> README states whether it's ready to run yet.

## How each recipe works

A recipe is a **directory**, not a module in a shared build — so you can copy one out and run it
in isolation. See [CONTRIBUTING.md](CONTRIBUTING.md) for the recipe anatomy.

## License

[Apache-2.0](LICENSE) — same as the library.
