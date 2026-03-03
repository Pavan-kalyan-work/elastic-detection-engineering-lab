# Telemetry Validation

## Objective
Validate successful ingestion of endpoint telemetry after Fleet enrollment.

## Validation Steps

- Confirm Elastic Agent status as Healthy in Fleet.
- Validate ingestion of process, network, and file events.
- Confirm ECS field normalization (process.name, process.parent.name, event.category).

## Observations

Telemetry was successfully ingested into Elasticsearch.

Process creation events were visible in Discover, confirming baseline visibility required for detection engineering.

## Engineering Insight

Detection logic must only be built after validating telemetry reliability and field accuracy.
