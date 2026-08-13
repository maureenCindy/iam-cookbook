# Contributing a recipe

A recipe teaches **one** access-control idea with the smallest app that makes the point obvious.
If a reader has to hold two new concepts in their head at once, it's two recipes.

## The recipe anatomy

Every recipe is a **self-contained directory**. It is *not* a subproject of a shared root build —
a reader must be able to copy the folder out and run it on its own.

```
NN-recipe-name/
├── README.md            # problem → IAM solution → gotchas (see below)
├── backend/             # a standalone Spring Boot app (its own Gradle wrapper)
│   └── ...
├── web/                 # OPTIONAL — only when the frontend is part of the lesson
│   └── ...
└── docker-compose.yml   # whatever infra the recipe needs (usually just Postgres)
```

### Rules

1. **Consume the published artifacts only** — `dev.mpofusindie:iam-bom:2.0.0` and
   `@mpofusindie/iam-react@^1.4.0`. Never `mavenLocal()` or a `file:` tarball; the recipe must
   match what a real adopter writes.
2. **Full-stack only when the frontend *is* the lesson.** If the point is server-side, adding a
   React app is noise — leave `web/` out. (Field masking and the React tour earn their `web/`;
   scoped access does not.)
3. **Prove the boundary with a test.** Runnable isn't enough. Every recipe ships at least one test
   that asserts the *allow* case passes **and** the *deny* case is refused (403/masked/scoped-out).
   That test is what makes the recipe trustworthy.
4. **One idea.** Resist bolting a second feature onto a working recipe — start a new one.
5. **Smallest domain that dramatizes the point.** Pick the domain so the lesson is obvious from
   the name: HR/salary for field masking, a clinic for scoping, a SaaS app for tenancy.

## The README shape

Each recipe's `README.md` follows the same skeleton so the repo reads consistently:

```markdown
# NN · Recipe Name

> One sentence: the problem this recipe solves.

**Stack:** Backend | Full-stack   **Status:** 🚧 not implemented / ✅ runnable

## The problem
The real-world scenario, in 2–3 sentences.

## The IAM solution
Which features, and *why these* over the alternatives.

## Run it
Copy-pasteable steps. Ends with a `curl` (or UI action) showing allow vs deny.

## The boundary this proves
Exactly what is allowed and what is refused — the thing the test asserts.

## Gotchas
The traps a first-time adopter hits (the interesting part).
```

## Naming

- Directories: `NN-kebab-case-name`, numbered to preserve the index arc.
- Docs: this repo follows the library's `UPPER-KEBAB-CASE.md` convention for any *extra* docs;
  `README.md` and `CONTRIBUTING.md` keep their standard names.
