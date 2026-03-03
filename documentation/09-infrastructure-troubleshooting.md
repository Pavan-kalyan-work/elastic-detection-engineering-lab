# Infrastructure Troubleshooting

## Objective

Document infrastructure-level challenges encountered during lab deployment and their impact on detection operations.

---

## Issue Observed

Elastic Stack services experienced inconsistent connectivity, affecting:

- Fleet enrollment
- Agent health status
- Telemetry ingestion reliability

---

## Investigation Process

- Verified Elasticsearch and Kibana service status.
- Checked open ports and service bindings.
- Reviewed Ubuntu network configuration.
- Compared Netplan configuration with NetworkManager settings.

---

## Root Cause

Conflict between Netplan and NetworkManager managing the same network interface resulted in unstable connectivity.

This directly impacted Fleet communication and endpoint telemetry flow.

---

## Resolution

- Standardized network management method.
- Ensured only one service controlled the interface.
- Restarted networking services.
- Revalidated Fleet server and endpoint connectivity.

---

## Engineering Insight

Detection engineering reliability depends on infrastructure stability.

Backend misconfiguration can silently affect:

- Agent enrollment
- Data ingestion
- Rule execution

Operational troubleshooting is a critical skill in SOC environments.
