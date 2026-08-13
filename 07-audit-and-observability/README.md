# 07 · Audit and observability

> Every authorization decision and admin change streams into **your own** audit ledger, and IAM's
> internals show up on a Prometheus scrape.

**Stack:** Backend   **Status:** 🚧 not implemented yet

## The problem
"Who granted this role, and when?" and "is the permission cache actually helping?" are production
questions. You need IAM's events in your system of record and its behavior on your dashboards —
without forking the library.

## The IAM solution
Implement the `IamAuditSink` SPI to receive audit events **after commit** and write them wherever you
keep your ledger. Bring a Micrometer registry (via actuator) and IAM's metrics light up on
`/actuator/prometheus`.

## Run it
_TBD — a host sink writing events to a table; trigger a grant and a denied request; show the rows and
the scraped metrics._

## The boundary this proves
An access decision / admin mutation produces exactly one audit event in the host ledger, delivered
after the originating transaction commits; metrics reflect real traffic.

## Gotchas
- Delivery is **after-commit**: a sink that writes to a DB must open its own unit of work — the
  original transaction is already gone.
- IAM ships Micrometer as `compileOnly`; without a host registry the meters silently no-op. Bringing
  actuator is the opt-in signal.
