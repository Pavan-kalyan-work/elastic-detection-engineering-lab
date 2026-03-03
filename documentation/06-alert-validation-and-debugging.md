# Alert Validation & Debugging

## Objective

Validate detection rule functionality and investigate alert generation failures during controlled testing.

---

## Scenario

A behavior-based rule detecting Office spawning PowerShell was deployed but did not initially generate alerts.

---

## Investigation Process

- Verified process event ingestion.
- Confirmed ECS field mapping:
  - process.name
  - process.parent.name
  - event.category
- Validated correct dataset:
  - logs-endpoint.events.process
- Reviewed detection rule execution schedule.
- Compared event timestamps with rule lookback configuration.

---

## Root Cause

Events were present in Elasticsearch but fell outside the configured rule lookback window.

This resulted in a silent false-negative scenario.

---

## Resolution

- Increased additional lookback time.
- Adjusted rule execution interval.
- Re-tested detection with controlled simulation.
- Confirmed successful alert generation.

---

## Engineering Insight

Detection reliability depends not only on correct logic but also on operational factors such as scheduling and ingestion latency.

Even correctly written rules can silently fail due to misconfigured time windows.
