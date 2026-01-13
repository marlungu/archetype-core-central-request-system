# Scripts

This folder contains developer utilities and operational helpers.

Examples:
- One-command local bootstrap
- Backfill helpers
- Data seeding and reset utilities
- Release and packaging helpers

Rules:
- Scripts should be safe by default and clearly documented.
- Core business logic does not live in scripts.
- Anything critical should be callable from CI and reproducible.
