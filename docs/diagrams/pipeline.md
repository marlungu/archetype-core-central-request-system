# V0 Pipeline Diagram

This diagram shows how request data moves through the system.

The goal is clarity, not complexity.

---

## High-level flow

[1] Data Generator  
(fake request records)
        |
        v
[2] Postgres (raw)
(what we received)
        |
        v
[3] dbt
(clean, connect, and decide truth)
        |
        v
[4] Postgres (serving)
(what we promise to consumers)
        |
        v
[5] API
(stable access for other systems)
        |
        v
[6] UI
(search and inspect requests)

---

### One rule to remember

- raw = what we got  
- staging = what we cleaned  
- core = what we believe  
- serving = what we promise  

Only the **serving** layer is exposed to consumers.


```mermaid
flowchart TD
  A[Data Generator] --> B[(Postgres<br/>raw)]
  B --> C[dbt<br/>clean + dedupe + classify]
  C --> D[(Postgres<br/>serving)]
  D --> E[API]
  E --> F[UI]
