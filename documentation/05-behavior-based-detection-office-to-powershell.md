# Behavior-Based Detection: Office Spawning PowerShell

## Objective

Develop a behavior-based detection rule identifying Microsoft Office applications spawning PowerShell processes to detect macro-driven or phishing-based execution chains.

---

## Threat Context

In enterprise environments, Microsoft Office applications rarely spawn PowerShell under legitimate conditions.

This pattern is commonly associated with:

- Malicious macro execution
- Phishing payload delivery
- Initial access techniques
- Execution of embedded scripts

---

## Detection Logic

Parent-child process correlation:

- `process.parent.name` = WINWORD.EXE OR EXCEL.EXE
- `process.name` = powershell.exe
- `event.category` = process

Dataset:
- `logs-endpoint.events.process`

---

## Validation Steps

- Confirmed correct dataset selection.
- Verified ECS field alignment.
- Simulated controlled execution to generate matching events.
- Validated event timestamps relative to detection schedule.

---

## Challenges Faced

- Initial alert failure due to rule lookback misconfiguration.
- Dataset confusion between process and non-process events.
- Need to validate case sensitivity and exact field values.

---

## False Positive Considerations

- Administrative scripting scenarios.
- IT automation tools invoking PowerShell from Office context.
- Legitimate add-ins triggering script execution.

Rule tuning requires contextual awareness to avoid excessive noise.

---

## MITRE ATT&CK Mapping

- T1204 – User Execution
- T1059.001 – PowerShell
- T1566 – Phishing

---

## Engineering Insight

Behavior-based detection improves resilience against payload variations and simple obfuscation techniques.

Parent-child process relationships provide stronger detection logic compared to static indicators such as file hashes or command strings.
