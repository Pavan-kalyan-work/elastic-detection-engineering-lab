# Lab Architecture

## Objective

Design and deploy an Elastic Stack-based SOC Detection Engineering lab simulating enterprise endpoint monitoring in a controlled environment.

---

## Architecture Components

- Ubuntu Server hosting:
  - Elasticsearch
  - Kibana
  - Fleet Server
- Windows 10 Endpoint running:
  - Elastic Agent
  - Elastic Defend integration

---

## Telemetry Flow

Windows Endpoint  
→ Elastic Agent  
→ Fleet Server  
→ Elasticsearch  
→ Kibana (Analysis & Detection Engine)

---

## Architecture Rationale

The architecture was designed to replicate a simplified enterprise SOC deployment where:

- Endpoints are centrally managed through Fleet
- Telemetry is normalized using ECS
- Detection rules operate on structured event streams
- Analysts investigate events within Kibana

---

## Engineering Goals

- Establish stable telemetry ingestion before detection development
- Validate agent health and data stream reliability
- Ensure ECS field normalization consistency
- Maintain infrastructure stability to prevent ingestion disruptions

---

## Operational Considerations

- Network stability directly impacts Fleet communication
- Time synchronization affects alert scheduling accuracy
- Dataset segmentation influences detection reliability
