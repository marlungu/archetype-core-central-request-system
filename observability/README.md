# Observability

This folder contains the monitoring and alerting assets required to operate the platform.

What we monitor:
- Pipeline runs (success rate, duration, failures)
- Data freshness and ingestion lag
- Row counts and unexpected volume changes
- Data quality failures (contract violations, quarantined records)
- API health (latency, error rates)

Artifacts:
- Dashboards (Grafana)
- Metrics definitions and collection config
- Alert rules and thresholds

Goal:
- Detect issues before consumers make decisions on stale or incorrect data.
