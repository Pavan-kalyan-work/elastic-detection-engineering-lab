# PowerShell Script Block Logging (Event ID 4104)

## Objective

Enhance logging visibility by enabling PowerShell Script Block Logging to capture full command content for deeper behavioral detection.

---

## Why This Was Needed

Default process creation logs only confirm that PowerShell executed.

They do not expose:

- Full command content
- Encoded or obfuscated payloads
- Inline script execution
- Post-exploitation logic

Deep visibility is required for:

- Encoded command detection
- Obfuscated script analysis
- Malicious macro execution chains
- Lateral movement preparation
- Privilege escalation attempts

---

## Configuration Steps

- Enabled **PowerShell Script Block Logging** via Group Policy.
- Verified generation of **Event ID 4104** in Windows Event Viewer.
- Confirmed ingestion into Elasticsearch.
- Validated presence of:
  - `powershell.file.script_block_text`
  - `event.code: 4104`
  - `process.name: powershell.exe`

---

## Challenges Faced

- Initial telemetry did not include full script content.
- Required confirmation that enhanced logging was successfully applied at the endpoint level.
- Field inspection was necessary to validate proper ECS mapping.

---

## Detection Engineering Impact

Enabling Script Block Logging significantly improved detection depth by allowing rule logic to inspect command content rather than relying solely on process execution events.

This enabled stronger behavior-based detection aligned with:

MITRE ATT&CK:
- T1059.001 – PowerShell
