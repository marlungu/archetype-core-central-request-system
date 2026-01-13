# ADR-002: V0 Technology Choices

## Status
Accepted

---

## Context

The Central Request System is a shared place where request data from many systems
can be collected, cleaned, and trusted.

Version 0 (V0) is focused on:
- being easy to understand
- having clear ownership boundaries
- running the same way on every machine
- keeping setup simple

Before adding pipelines, transformations, or services, the system needs a
stable and repeatable way to run.

---

## Decision

For V0, the system will use:
- Postgres as the main place where data lives
- docker-compose to run services locally
- a local-first setup for development and testing

---

## Rationale

### Why Postgres

Postgres is the main place where data lives in V0.

We use it to:
- store incoming data
- clean and organize that data
- decide which records represent the same real request
- share clean, stable data with the API and UI

Postgres acts as the warehouse for V0.

It is a regular relational database, not a large cloud warehouse like Redshift,
but it is strong enough for this stage of the project.

Postgres supports:
- multiple schemas (raw, staging, core, serving)
- clear data rules and constraints
- predictable behavior that is easy to reason about
- smooth integration with dbt

We intentionally avoid warehouse-specific features that would:
- make local setup harder
- add complexity without helping V0 goals

If the system grows, the data can later move to a larger warehouse
without changing how the rest of the system works.

---

### Why docker-compose

docker-compose is used to:
- run the system the same way on every machine
- clearly define which services exist and how they connect
- avoid hidden setup steps on a developer’s computer

This lets anyone run the system without needing a cloud account
or special environment setup.

---

### Why local-first execution

Running everything locally:
- makes it easier to test changes quickly
- makes bugs easier to reproduce
- lowers the barrier for contributors
- helps validate the system design before adding scale

V0 is about getting the design right, not handling large volumes of data.

---

## Consequences

- Anyone can run the system locally
- Setup stays simple and predictable
- Scaling is intentionally postponed until the design is proven

This trades early scale for clarity and confidence.

---

## Alternatives Considered

### Starting with a cloud warehouse (for example, Redshift)

This was not chosen for V0 because:
- it adds setup and cost early
- it makes local development harder
- it does not improve the core design decisions being tested

---

## Criteria for Reconsideration

This decision will be revisited when:
- the data becomes too large for Postgres
- many consumers need to query the data at the same time
- the system needs to run in production
- warehouse-specific features clearly add value

At that point, a warehouse like Redshift can replace Postgres
without changing the rest of the system.

---

## Notes

V0 is focused on proving the system design.

Future ADRs may cover scaling, deployment, and cloud-specific choices.
