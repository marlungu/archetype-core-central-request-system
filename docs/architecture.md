# Architecture
## Archetype Core | Central Request System

This document describes the high-level architecture and ownership boundaries of the Central Request System. It explains what each component is responsible for, how data flows through the system, and how the platform is operated safely.

For the business case, guarantees, and non-goals, see `docs/problem-brief.md`.

---

## 1) System overview

The Central Request System is a reference data platform that consolidates request records from multiple systems into a single canonical representation.

The platform is intentionally designed for reliability:
- deterministic deduplication
- consistent classification
- stable serving schemas
- observable operations

Consumers interact with serving datasets through supported interfaces, not raw source data.

---

## 2) Components

### 2.1 Source systems (simulated in V0)
- Purpose: produce request records with different identifiers, schemas, and update patterns.
- V0: a simulator generates request events and schema variations to create realistic edge cases.

Ownership: external to this platform.

---

### 2.2 Pipelines (ingestion + orchestration)
Location: `/pipelines`

Responsibilities:
- ingest request records from sources (or the simulator)
- land records into raw tables in the warehouse
- ensure idempotency (re-runs do not duplicate)
- record run metadata (start/end, counts, status, errors)
- support backfills and reprocessing

Non-responsibilities:
- no business classification logic
- no deduplication logic that affects canonical state
- no serving-layer reshaping for consumer convenience

Output:
- raw landed tables in the warehouse (immutable snapshots preferred)

---

### 2.3 Central Data Store (system of record)
V0 target: Postgres (local-first)

The Central Data Store holds the authoritative representation of canonical
request data and supports analytical querying for downstream systems.

In V0, Postgres is used to:
- store raw, staging, core, and serving datasets
- enforce data contracts and constraints
- support deterministic transformations and queries
- provide a reliable backing store for APIs and inspection tools

While Postgres is not a distributed data warehouse, it provides sufficient
analytical capability for V0 and allows the architecture to be validated
without introducing unnecessary infrastructure complexity.

The abstraction is intentional:
the Central Data Store can later be backed by a data warehouse such as
Redshift or Snowflake without changing upstream or downstream contracts.

Schemas (logical layers):
- `raw`      landed source tables
- `staging`  normalized and typed models
- `core`     canonical entities (request)
- `serving`  stable consumption tables for the API/UI

The Central Data Store is the source of truth for canonical request state.
