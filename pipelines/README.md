# Pipelines

This folder owns ingestion and orchestration.

Responsibilities:
- Pull or receive records from source systems (or the simulator)
- Write immutable raw snapshots for audit and replay
- Load landing tables in the warehouse
- Ensure idempotency (re-runs do not create duplicates)
- Capture run metadata (counts, timestamps, status) for operations

Non-responsibilities:
- Business classification rules live in dbt models, not in ingestion code.
- Serving logic belongs in the API, not in pipelines.
