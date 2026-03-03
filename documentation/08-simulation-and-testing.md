# Simulation and Testing

## Objective

Validate detection logic through controlled simulation of suspicious behavior.

---

## Scenario Tested

Simulated Microsoft Office spawning PowerShell to trigger behavior-based detection logic.

Testing methods included:

- Manual execution of PowerShell from Office context.
- Controlled command execution resembling macro-triggered activity.
- Timestamp comparison against detection rule schedule.

---

## Challenges Encountered

- Security controls limited macro execution.
- Controlled simulation did not always align with rule lookback window.
- Some executions were blocked before full telemetry generation.

---

## Observations

- Parent-child process visibility was confirmed via:
  - process.name
  - process.parent.name
- Successful detection required correct dataset alignment and time-window configuration.

---

## Engineering Insight

Testing detections requires controlled behavioral simulation.

Detection development must account for:
- Execution timing
- Telemetry ingestion delay
- Security control interference
