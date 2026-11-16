# Lotbook

Inventory and sales accounting for small resale and maker businesses: purchase lots, stock ledger, production from components, sales with marketplace fees, returns, stock-takes, and a price calculator.

> **Status:** early development (stage 0 — repository and domain design). See [`docs/STATUS.md`](docs/STATUS.md).

## Why this project exists

Lotbook is a learning project built step by step, and also a real tool for tracking goods bought in batches (for example from any market), items used in assemblies, and products sold on marketplaces.


## Planned stack

- Backend: NestJS, PostgreSQL (Prisma), Redis, RabbitMQ, MinIO
- Mobile: React Native (Expo)
- Optional web admin: Angular
- Infra: Docker Compose, GitHub Actions
- Observability: pino, Prometheus, Grafana, OpenTelemetry, Sentry

## Documentation

| Doc | Purpose |
|---|---|
| [`docs/plan.md`](docs/plan.md) | Master plan: goals, architecture, stages |
| [`docs/STATUS.md`](docs/STATUS.md) | Where the project is right now |
| [`docs/workflow.md`](docs/workflow.md) | How to work on the project (git cycle, docs rules) |
| [`docs/stages/`](docs/stages) | Detailed plan for each stage |
| [`docs/adr/`](docs/adr) | Architecture decision records |
| [`docs/domain.md`](docs/domain.md) | Domain glossary |
| [`docs/devlog/`](docs/devlog) | Session notes |
| [`CLAUDE.md`](CLAUDE.md) | Instructions for the coding agent |

## License

TBD.
