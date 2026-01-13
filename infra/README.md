# Infra

This folder contains everything needed to run the system in a repeatable way.

Includes:
- Local development stack (docker-compose)
- Environment configuration patterns (dev, stage, prod)
- Infrastructure-as-code (optional later), when moving beyond local

Boundaries:
- Infra defines how services run, connect, and are configured.
- Business logic never lives here.

Status:
- V0 uses a local docker-compose setup.
