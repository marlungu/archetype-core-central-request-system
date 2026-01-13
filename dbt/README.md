# dbt

This folder owns transformation, deduplication, classification, and published serving tables.

Model layers:
- raw: landed source tables (minimal assumptions)
- staging: cleaned types, normalized fields, standardized timestamps
- core: canonical entities with stable keys and history handling
- serving: stable, documented tables intended for consumption

Quality:
- dbt tests act as contracts (uniqueness, not null, relationships, accepted values).
- Incremental models are preferred where appropriate.

Rules:
- Deduplication is deterministic and documented.
- Classification rules are explicit, versionable, and testable.
