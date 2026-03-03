# Elastic Stack SOC Detection Engineering Lab

> Hands-on SOC Detection Engineering case study built using Elastic Stack.  
> Demonstrates telemetry validation, behavior-based detection development, alert debugging, dataset analysis, and infrastructure troubleshooting in a simulated enterprise environment.

## Overview

Designed and implemented an end-to-end SOC Detection Engineering lab using the Elastic Stack to simulate enterprise-grade endpoint monitoring.

The project focuses on structured telemetry validation, behavior-based detection logic, alert debugging, dataset-level analysis, and infrastructure troubleshooting.

## Technical Skills Demonstrated

- Elastic Stack (Elasticsearch, Kibana, Fleet, Elastic Defend)
- Windows Event Log Analysis
- ECS Field Validation
- Detection Rule Development
- MITRE ATT&CK Mapping
- Alert Time-Window Debugging
- Dataset Troubleshooting
- Linux Network Configuration (Netplan)

## Lab Environment

- Ubuntu Server hosting Elasticsearch, Kibana, Fleet
- Windows 10 endpoint with Elastic Agent
- Elastic Defend enabled
- Custom detection rules deployed and validated

---

## Key Engineering Achievements

- Built behavior-based detection (Office spawning PowerShell)
- Mapped detections to MITRE ATT&CK techniques
- Enabled and validated PowerShell Script Block Logging (Event ID 4104)
- Debugged time-window related false-negative alerts
- Resolved dataset misalignment (process vs library events)
- Conducted controlled detection simulation testing
- Troubleshot Ubuntu Netplan & NetworkManager conflict affecting telemetry ingestion

---

## Detection Techniques Covered

- T1059.001 – PowerShell
- T1204 – User Execution
- T1566 – Phishing
- Parent-child process analysis
- Behavior-based detection engineering

---

## Documentation Structure

Detailed documentation is available in the `documentation/` folder:

1. Project Overview  
2. Lab Architecture  
3. Telemetry Validation  
4. Logging Maturity  
5. Detection Engineering  
6. Alert Validation & Debugging  
7. Dataset Analysis  
8. Simulation & Testing  
9. Infrastructure Troubleshooting  

---

## Screenshots (To Be Added)

- Fleet Agent Healthy Status  
- Detection Rule Configuration  
- Triggered Alert View  
- Discover Query Validation  

---

## Purpose

This project demonstrates practical detection engineering capability, including rule development, operational validation, and troubleshooting beyond standard alert monitoring.

It reflects hands-on SOC-level thinking rather than theoretical study.

## Professional Outcome

This project reflects readiness for:

- SOC Analyst (L1) roles
- Security Monitoring roles
- Entry-level Detection Engineering exposure

It demonstrates the ability to move beyond alert monitoring into structured detection development and troubleshooting.
