# Elastic Stack SOC Detection Engineering Lab

## Overview

This project documents an end-to-end SOC Detection Engineering lab built using the Elastic Stack.

The lab simulates enterprise endpoint monitoring and demonstrates structured detection development, telemetry validation, alert debugging, dataset analysis, and infrastructure troubleshooting.

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

This project demonstrates hands-on detection engineering capability beyond basic alert monitoring and reflects structured SOC-level investigation and troubleshooting thinking.
