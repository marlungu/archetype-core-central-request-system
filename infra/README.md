# Infrastructure

This folder defines how the Central Request System is run in a repeatable, predictable way across environments.

Infrastructure concerns are intentionally separated from application logic to preserve clear ownership boundaries.

---

## What lives here

- Local runtime configuration (docker-compose)
- Environment configuration patterns (local, stage, prod)
- Service connectivity and lifecycle definitions
- Health checks and startup ordering

---

## What does not live here

- Business logic
- Data transformation rules
- Deduplication or classification logic
- Application-level workflows

These concerns belong to pipelines, dbt, and services.

---

## Design principles

- Local-first execution for fast iteration and reproducibility
- Minimal infrastructure in V0 to validate architecture
- Explicit configuration over implicit defaults
- Infrastructure remains replaceable without changing system contracts

---

## Status

- V0 uses a local docker-compose setup with Postgres as the Central Data Store
- Stage/prod infrastructure and IaC are intentionally deferred
