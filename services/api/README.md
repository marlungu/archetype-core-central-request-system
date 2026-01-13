# API Service

This service exposes stable, versioned access to serving datasets.

Endpoints:
- Read: retrieve a request by canonical ID
- Search: filter requests by status, type, priority, date range

Principles:
- Versioned routes (v1, v2) to protect consumers.
- Read-only in V0.
- The source of truth is the warehouse serving schema.

