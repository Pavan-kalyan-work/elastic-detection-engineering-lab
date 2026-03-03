# Alert Validation & Debugging

## Objective

Validate detection rule functionality and systematically investigate alert generation failures during controlled simulation.

---

## Scenario

A behavior-based rule detecting Office spawning PowerShell was deployed but did not initially generate alerts despite visible matching events in Discover.

---

## Investigation Process

- Verified process event ingestion.
- Confirmed ECS field mapping:
  - `process.name`
  - `process.parent.name`
  - `event.category`
- Validated correct dataset:
  - `logs-endpoint.events.process`
- Reviewed detection rule schedule (execution interval and additional lookback time).
- Compared event `@timestamp` with rule execution window.
- Confirmed ingestion latency impact.

---

## Root Cause

Events were present in Elasticsearch but fell outside the configured rule lookback window.

The detection rule execution interval did not align with the event generation time, resulting in a silent false-negative condition.

---

## Resolution

- Increased additional lookback time.
- Adjusted rule execution interval.
- Re-tested detection using controlled simulation.
- Confirmed alert generation in the Security alerts index.
- Verified alert details matched expected parent-child process behavior.

---

## Challenges Faced

- Initial assumption that rule logic was incorrect.
- Overlooked operational configuration (scheduling vs logic).
- Required careful timestamp comparison and rule execution review.

---

## Engineering Insight

Detection reliability depends not only on correct query logic but also on operational configuration.

Key operational factors include:

- Rule scheduling interval
- Ingestion latency
- Time synchronization
- Dataset alignment

Operational misconfiguration can invalidate otherwise correct detection rules, leading to silent failures in production SOC environments.
