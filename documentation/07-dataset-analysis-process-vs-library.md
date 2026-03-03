# Dataset Analysis: Process vs Library Event Confusion

## Objective

Investigate dataset-level discrepancies encountered during detection rule validation.

---

## Issue Observed

Detection logic appeared correct, but query results were inconsistent across different data views.

Process activity was visible in Discover, yet rule behavior did not align with expectations.

---

## Investigation Steps

- Reviewed `event.dataset` values.
- Compared:
  - logs-endpoint.events.process
  - logs-endpoint.events.library
- Validated `data_stream.dataset` field.
- Inspected ECS field consistency.

---

## Root Cause

Detection logic initially referenced an incorrect dataset.

Endpoint telemetry includes multiple event streams, and misalignment between dataset selection and rule configuration resulted in detection inconsistency.

---

## Resolution

- Corrected dataset reference to:
  logs-endpoint.events.process
- Re-validated rule execution.
- Confirmed expected behavior.

---

## Engineering Insight

Understanding dataset segmentation within Elastic is critical for accurate detection development.

Misconfigured dataset targeting can produce silent detection failures even when logic is technically correct.
