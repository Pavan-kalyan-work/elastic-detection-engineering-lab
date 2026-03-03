# Simulation and Testing

## Objective

Validate detection logic through controlled simulation of suspicious behavior and confirm alert reliability under operational conditions.

---

## Scenario Tested

Simulated Microsoft Office spawning PowerShell to trigger the behavior-based detection rule.

Testing approaches included:

- Manual execution of PowerShell from an Office process context.
- Controlled command execution mimicking macro-triggered activity.
- Validation of event timestamps against rule execution interval.
- Repeated testing to confirm consistency.

---

## Validation Steps

- Confirmed event generation in Discover.
- Verified:
  - `process.name`
  - `process.parent.name`
  - `event.category`
- Checked dataset alignment:
  - `logs-endpoint.events.process`
- Confirmed alert creation in Security alerts index.
- Reviewed alert metadata for parent-child accuracy.

---

## Challenges Encountered

- Security controls limited certain macro execution scenarios.
- Simulation timing did not always align with rule lookback window.
- Some executions were blocked before full telemetry ingestion.
- Required multiple controlled attempts for consistent validation.

---

## Observations

- Parent-child process visibility provided reliable behavioral indicators.
- Alert reliability depended on scheduling configuration and ingestion latency.
- Controlled simulation improved confidence in detection stability.

---

## Engineering Insight

Testing detections requires structured behavioral simulation rather than single-instance execution.

Detection development must account for:

- Execution timing
- Telemetry ingestion delay
- Dataset alignment
- Rule scheduling configuration
- Security control interference

Reliable detection engineering requires repeatable validation, not assumption-based confidence.
