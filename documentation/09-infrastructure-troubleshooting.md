# Infrastructure Troubleshooting

## Objective

Document infrastructure-level challenges encountered during lab deployment and analyze their impact on detection operations and telemetry reliability.

---

## Issue Observed

Elastic Stack services experienced inconsistent connectivity, affecting:

- Fleet enrollment stability
- Agent health status (intermittent offline state)
- Telemetry ingestion reliability
- Detection rule consistency

Endpoint communication with Fleet was unstable, resulting in delayed or missing telemetry.

---

## Investigation Process

- Verified Elasticsearch and Kibana service status using `systemctl`.
- Confirmed open ports and service bindings (`9200`, `5601`, Fleet port).
- Validated network interface configuration.
- Reviewed Ubuntu Netplan configuration.
- Compared Netplan settings with NetworkManager control.
- Tested connectivity between endpoint and server.
- Monitored Fleet agent heartbeat behavior.

---

## Root Cause

A configuration conflict between Netplan and NetworkManager managing the same network interface caused unstable connectivity.

Dual control over the interface resulted in intermittent network resets, directly impacting:

- Fleet server communication
- Endpoint telemetry flow
- Detection evaluation timing

---

## Resolution

- Standardized network management to a single controller.
- Disabled conflicting service.
- Restarted networking services.
- Revalidated:
  - Fleet server connectivity
  - Agent healthy status
  - Continuous telemetry ingestion
- Monitored stability over multiple rule execution cycles.

---

## Challenges Faced

- Initial assumption that issue was Elastic service-related.
- Required separation of application-layer troubleshooting from network-layer troubleshooting.
- Intermittent behavior made issue identification non-trivial.

---

## Engineering Insight

Detection engineering reliability depends heavily on infrastructure stability.

Backend misconfiguration can silently affect:

- Agent enrollment
- Telemetry ingestion consistency
- Rule execution timing
- Alert reliability

Operational troubleshooting across both application and network layers is a critical skill in real-world SOC environments.
