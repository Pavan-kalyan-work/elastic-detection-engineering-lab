# Telemetry Validation

## Objective

Validate successful ingestion, normalization, and visibility of endpoint telemetry following Fleet enrollment.

---

## Validation Steps

- Confirm Elastic Agent status as **Healthy** within Fleet.
- Validate ingestion of process, network, and file events.
- Confirm correct ECS field normalization:
  - `process.name`
  - `process.parent.name`
  - `event.category`
  - `host.name`
  - `user.name`
- Verify timestamp consistency (`@timestamp`) for detection scheduling reliability.

---

## Observations

Telemetry was successfully ingested into Elasticsearch.

Process creation events were visible in Discover, confirming baseline visibility required for detection engineering.

Network and file-related events were also confirmed within the appropriate datasets.

---

## Challenges Faced

- Initial uncertainty regarding correct dataset mapping (`process` vs `library` events).
- Field naming validation required careful ECS inspection.
- Delay between event generation and ingestion required timestamp verification.

---

## Engineering Insight

Detection logic must only be developed after validating telemetry reliability and ECS field accuracy.

Incorrect field assumptions or dataset misinterpretation can result in silent detection failures despite correct rule logic.

Telemetry validation is a foundational detection engineering step, not a post-deployment task.
