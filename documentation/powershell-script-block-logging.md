# PowerShell Script Block Logging (Event ID 4104)

## Objective
Enhance logging visibility by enabling PowerShell Script Block Logging to capture full command content.

## Why This Was Needed
Process creation logs only show that PowerShell executed.
They do not reveal the full script content.

Deep visibility is required for:
- Encoded commands
- Obfuscated scripts
- Post-exploitation activity
- Malicious macro execution chains

## Configuration Steps
- Enabled Script Block Logging via Group Policy.
- Verified Event ID 4104 generation.
- Confirmed ingestion into Elasticsearch.

## Detection Engineering Impact
This significantly improved detection capability for:

MITRE ATT&CK:
- T1059.001 – PowerShell
