# Architecture Decision Records

One file per decision: `NNNN-short-title.md`, based on [`0000-template.md`](0000-template.md). Written in English.

Status values: `proposed`, `accepted`, `superseded`.

| # | Decision | Status |
|---|---|---|
| 0001 | Inventory valuation method (FIFO by lots vs average) | proposed |
| 0002 | Money storage (integer minor units + currency, rounding rules) | proposed |
| 0003 | Multi-tenancy model (`tenant_id`, optional RLS) | proposed |
| 0004 | Ledger design (append-only, compensating movements, balance cache) | proposed |
| 0005 | Identifiers (UUID v7, client-generated for drafts) | proposed |
| 0006 | Broker and cache roles (RabbitMQ vs Redis) | proposed |
| 0007 | Outbox pattern and consumer idempotency | proposed |
| 0008 | Authentication library (after spike) | proposed |
| 0009 | Document rendering (HTML to PDF tool) | proposed |
| 0010 | API contract approach (OpenAPI-first vs code-first) | proposed |
| 0011 | Negative stock policy | proposed |
| 0012 | Deployment strategy | proposed |
| 0013 | CQRS scope (CQRS-lite where, and where not) | proposed |
| 0014 | RBAC model and hiding sensitive fields | proposed |
