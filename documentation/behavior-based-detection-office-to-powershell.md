# Behavior-Based Detection: Office Spawning PowerShell

## Objective
Develop a behavior-based detection rule identifying Microsoft Office applications spawning PowerShell processes.

## Threat Context
In enterprise environments, Office applications rarely spawn PowerShell during normal activity.

This pattern is commonly associated with:
- Malicious macro execution
- Phishing payload delivery
- Initial access techniques

## Detection Logic Concept

Monitor:

- process.parent.name = WINWORD.EXE OR EXCEL.EXE
- process.name = powershell.exe

## MITRE ATT&CK Mapping

- T1204 – User Execution
- T1059.001 – PowerShell
- T1566 – Phishing

## Engineering Considerations

- Validate correct dataset (logs-endpoint.events.process)
- Confirm ECS field alignment
- Test detection with controlled simulation
- Monitor for false positives

## Insight

Behavior-based detection provides stronger coverage than static indicators and improves resilience against minor payload variations.
