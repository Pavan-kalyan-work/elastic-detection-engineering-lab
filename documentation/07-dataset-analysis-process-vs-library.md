# Dataset Analysis: Process vs Library Event Confusion

## Objective

Investigate dataset-level discrepancies encountered during detection rule validation and ensure correct data stream alignment.

---

## Issue Observed

Detection logic appeared technically correct, but query results were inconsistent across different data views.

Process activity was visible in Discover, yet the detection rule did not consistently evaluate matching events.

---

## Investigation Steps

- Reviewed `event.dataset` values across indexed events.
- Compared:
  - `logs-endpoint.events.process`
  - `logs-endpoint.events.library`
- Validated `data_stream.dataset` field in raw event JSON.
- Confirmed `event.category: process` alignment.
- Cross-checked index pattern used by detection rule.

---

## Root Cause

Detection logic initially referenced an incorrect dataset.

Elastic Endpoint telemetry is segmented into multiple event streams (process, file, network, library, etc.).

Misalignment between dataset selection and detection rule configuration resulted in incomplete rule evaluation and inconsistent alert behavior.

---

## Resolution

- Corrected dataset reference to:
  `logs-endpoint.events.process`
- Revalidated rule execution with controlled simulation.
- Confirmed consistent event evaluation and alert triggering.

---

## Challenges Faced

- Initial assumption that rule logic was flawed.
- Overlooked the impact of dataset segmentation on detection queries.
- Required raw event inspection to identify correct data stream.

---

## Engineering Insight

Understanding dataset segmentation within Elastic is critical for accurate detection engineering.

Incorrect dataset targeting can silently exclude relevant telemetry, resulting in detection gaps despite correct rule logic.

Dataset awareness is essential when building reliable, production-ready detection rules.
