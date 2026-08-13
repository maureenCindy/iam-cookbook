# 06 · Add IAM to an existing app

> You already have a Spring Boot app with your own JPA entities and Flyway migrations. Add the IAM
> starter — and watch nothing of yours break.

**Stack:** Backend   **Status:** 🚧 not implemented yet

## The problem
The scariest moment adopting any framework: does dropping it onto the classpath hijack your JPA
scanning, clobber your Flyway history, or override your config? For most access-control libraries the
honest answer is "maybe."

## The IAM solution
The starter is built to **coexist**: it joins your app's default component scanning additively (your
entities and repositories keep working), runs its own Flyway history without touching yours, and
leaves your base config alone. This recipe also shows the **contract-only module** pattern — a
business module that depends on `dev.mpofusindie:iam-api` for `@RequiresPermission` and nothing else,
keeping the engine off its compile path.

## Run it
_TBD — start the "inventory" app standalone (its own entity + migration + repository), add the IAM
starter, show both the host's endpoints and IAM's admin plane working side by side._

## The boundary this proves
Host repositories/entities still wire; host migrations still run; IAM's tables and enforcement are
present too — no collision in either direction.

## Gotchas
- The starter uses `@AutoConfigurationPackage` (not `@EntityScan`) precisely so it doesn't replace
  your scanning — the trap that broke real hosts before it was fixed.
- IAM runs its **own** Flyway instance/history; your `spring.flyway.*` stays yours.
- The contract module compiles against `iam-api` only; the engine is provided at runtime by the
  starter in the app module.
