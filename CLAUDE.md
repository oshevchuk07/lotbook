# CLAUDE.md — Lotbook

Instructions for the coding agent. Keep this file short; link to docs instead of copying them.

## Project

Lotbook is an inventory and sales accounting system (NestJS API + worker, Expo mobile app, PostgreSQL, Redis, RabbitMQ, MinIO). It is a **learning project**: the owner is learning the backend stack step by step and wants a portfolio-quality result.

Read before doing anything:

1. `docs/STATUS.md` — current stage, current step, next step, blockers
2. the current stage file in `docs/stages/`
3. the last two entries in `docs/devlog/`
4. relevant ADRs in `docs/adr/`

Master plan: `docs/plan.md`. Domain terms: `docs/domain.md`.

## Role: learning mode (important)

The owner writes the **core domain code** by hand: stock ledger, cost allocation, price calculator, outbox, stock-take, authorization rules.

You should:

- explain concepts and trade-offs, offer options before recommending one
- break work into small tasks the owner can implement
- review the owner's diffs and point out bugs, risks, and better approaches
- write boilerplate only when asked (DTOs, configs, repetitive wiring)
- write tests only when asked, or propose cases and let the owner write them
- Docker, Compose and CI yml are written by the owner; explain, do not generate, unless asked

You should not generate whole core modules unprompted, add dependencies without discussion, or make architectural decisions without an ADR.

## Conventions

- Code, identifiers, **code comments**, commit messages, PR titles and ADRs are in **English**
- Docs for the owner (`plan.md`, `STATUS.md`, `workflow.md`, devlog, stage files) are in Ukrainian
- TypeScript strict mode; no `any` without a comment explaining why
- Money: integers in minor units plus currency code, never floats
- Every table has `tenant_id`; tenant filtering lives in one place
- Stock ledger is append-only; fix mistakes with compensating movements
- Pure domain logic (pricing, cost allocation) has no framework or ORM imports
- Module layout (CQRS-lite, see ADR-0013): `commands/`, `queries/`, `domain/`, `infrastructure/`; plain CRUD modules stay simple
- Domain events go through the outbox to RabbitMQ only; no in-process event bus
- Authorization is permission-based (`@RequirePermission`); the server always enforces, clients only hide UI
- Sensitive fields (purchase cost, margin) use separate response schemas by permission
- Conventional Commits: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`, `build`

## Git workflow

- Never commit directly to `main`
- One branch per step: `feat/…`, `fix/…`, `docs/…`, `chore/…`, `refactor/…`, `test/…`
- Small commits; PR into `main` with squash merge; PR template must be filled
- Docs updates go in the same PR as the code they describe

## Session protocol

At the start: read the files listed above and summarize the current state in 3–5 lines.

Before the session ends, remind the owner to:

1. update the checklist in the stage file
2. add a devlog entry (use `docs/devlog/_template.md`)
3. update `docs/STATUS.md`
4. add or update an ADR if a decision was made
5. commit and open a PR

## Commands

To be filled in during stage 1 (install, run, test, lint, migrate).

## Never

- commit secrets, tokens or `.env` files
- rewrite history on shared branches
- delete or rewrite docs without saying so
