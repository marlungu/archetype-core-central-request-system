# archetype-core-central-request-system
Each folder contains a README describing its responsibilities and boundaries.

---

## Design philosophy

This system is built according to the following principles:

- clarity over cleverness
- explicit boundaries over implicit coupling
- documented tradeoffs over hidden assumptions
- stability for consumers over convenience for producers

The goal is to make the system predictable, explainable, and safe to depend on.

---

## How to read this repository

If you are new to this repository, start here:

1. `docs/problem-brief.md`  
   The authoritative description of the business problem, guarantees,
   and non-goals.

2. `docs/architecture.md`  
   High-level system design and data flow (added incrementally).

3. Component READMEs  
   Each major folder explains what belongs there and what does not.

---

## Status

This project is developed incrementally as part of **Archetype Core by Mariana Lungu**.

The initial version focuses on:
- a single request source
- a canonical request model
- deterministic deduplication
- a minimal serving interface

Additional sources, serving patterns, and operational features are introduced
deliberately over time.

---

## About Archetype Core

Archetype Core is a body of work focused on how complex data systems should be designed when scale, correctness, and decision-making matter.

This repository serves as a concrete reference system that makes those design principles tangible.
