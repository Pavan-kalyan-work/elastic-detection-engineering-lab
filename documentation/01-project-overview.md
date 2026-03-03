# Project Overview

## Title  
Elastic Stack SOC Detection Engineering Lab

## Objective

Design, deploy, and operationalize a Detection Engineering lab using the Elastic Stack to simulate enterprise-grade endpoint monitoring and behavior-based threat detection.

This project was built to move beyond basic SIEM monitoring and demonstrate structured detection development, telemetry validation, and troubleshooting maturity.

---

## Problem Statement

Many SOC environments rely heavily on alert monitoring without validating:

- Telemetry reliability
- Dataset correctness
- Logging depth
- Detection scheduling configuration

This lab was designed to simulate real-world challenges faced during detection engineering and SOC operations.

---

## Scope of Implementation

The project includes:

- Lab architecture design (Ubuntu + Windows endpoint)
- Fleet-managed Elastic Agent enrollment
- Telemetry validation and ECS field inspection
- PowerShell Script Block Logging (Event ID 4104) enablement
- Behavior-based detection development (Office spawning PowerShell)
- MITRE ATT&CK technique mapping
- Alert validation and time-window debugging
- Dataset misconfiguration troubleshooting
- Operational reasoning and investigation documentation

---

## Tools & Technologies

- Elasticsearch
- Kibana
- Fleet
- Elastic Defend
- Windows 10 Endpoint
- Ubuntu Server

---

## Detection Engineering Goals

- Validate telemetry before detection creation
- Build behavior-based detection logic rather than signature-only rules
- Map detections to MITRE ATT&CK techniques
- Investigate detection failures systematically
- Document operational and infrastructure challenges

---

## MITRE ATT&CK Techniques Covered

- T1059.001 – PowerShell
- T1204 – User Execution
- T1566 – Phishing
- T1110 – Brute Force (planned testing scope)
- T1078 – Valid Accounts (planned analysis scope)

---

## Outcome

This project demonstrates:

- Detection engineering mindset
- Operational troubleshooting capability
- Dataset-level analysis awareness
- Rule scheduling and time-window debugging
- Structured SOC documentation practices

The lab reflects hands-on engineering work rather than theoretical study.
