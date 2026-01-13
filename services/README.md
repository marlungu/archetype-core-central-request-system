# Services

This folder contains production services that expose the platform to consumers.

Primary service:
- API service that provides a stable interface to serving data

Responsibilities:
- Serve canonical request data through versioned endpoints
- Enforce access patterns (consumers should not query raw tables directly)
- Provide health endpoints for operations

Non-responsibilities:
- The API does not transform raw data. That is dbt's job.
- The API does not implement business workflows. It exposes data safely.
