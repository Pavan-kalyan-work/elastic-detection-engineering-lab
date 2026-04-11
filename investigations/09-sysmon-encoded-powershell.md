# 🔐 SOC Investigation Report: PowerShell Encoded Command Detection (Sysmon Enhanced)

This report documents a SOC investigation analyzing encoded PowerShell execution using Sysmon-enhanced logging to improve visibility and detection accuracy.

---

## 📌 Summary

A suspicious PowerShell execution was detected involving an encoded command (`-enc` flag). This technique is commonly used by attackers to obfuscate malicious scripts.

With Sysmon-enabled process creation logging, full command-line visibility allowed accurate detection, investigation, and validation of this behavior.

---

## 🖥️ Environment

- **SIEM:** Elastic Stack (Elasticsearch, Kibana, Fleet, Elastic Defend)  
- **Endpoint:** Windows 10 Virtual Machine  
- **Logging Enhancement:** Sysmon (Event ID 1 – Process Creation)  
- **User:** kalyan  
- **Host:** desktop-qucd21v  

---

## 🚨 Detection Details

### 🔹 Rule Name:
**Suspicious PowerShell Encoded Command**

### 🔹 Detection Logic:

```
process.name: "powershell.exe" AND process.args: "-enc"
```

### 🔹 MITRE ATT&CK Mapping:

- **Tactic:** Execution (TA0002)  
- **Technique:** T1059.001 – PowerShell  

---

## 🔍 Investigation Steps

### 1. Log Analysis

Filtered process creation events:

```
event.code: 1 AND process.name: "powershell.exe"
```

Reviewed command-line arguments for suspicious indicators.

---

### 2. Key Fields Observed

- **process.name:** powershell.exe  
- **process.command_line:**  
  `"C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -enc SQBFAFgA`  
- **process.args:** -enc  
- **user.name:** kalyan  
- **host.name:** desktop-qucd21v  

---

### 3. Behavior Identification

- PowerShell executed with encoded command  
- Base64 string used to obfuscate execution  
- Command initiated from user session  

---

## ⏱️ Timeline Reconstruction

```
1. User "kalyan" executed PowerShell  
2. PowerShell launched with -enc flag  
3. Encoded payload executed  
4. Detection rule triggered alert  
```

---

## 🧠 Behavioral Analysis

### 🔹 Observed Behavior

```
powershell.exe → encoded execution (-enc)
```

### 🔹 Interpretation

- Encoded commands are commonly used to:

  - Hide malicious payloads  
  - Bypass detection mechanisms  
  - Execute obfuscated scripts  

- This technique is widely observed in:

  - Malware execution  
  - Phishing attacks  
  - Post-exploitation frameworks  

Sysmon enhances detection by providing full command-line visibility, which is critical for identifying such obfuscation techniques.

---

## ⚖️ Analysis & Findings

### 🔹 Indicators

- Use of `-enc` flag  
- Obfuscated command execution  
- User-initiated PowerShell activity  

### 🔹 Context Evaluation

- Activity simulated in controlled lab environment  
- Encoded payload was not fully malicious  
- Behavior aligns with real-world attacker techniques  

---

## 🧭 MITRE ATT&CK Mapping

- T1059.001 – PowerShell  

---

## 🧾 Final Classification

```
Suspicious Activity → Malicious Technique Observed
```

---

## 🚀 SOC Analyst Decision

- **Severity:** High  
- **Action Taken:** Alert validated and documented  

### 🔹 Recommended Actions (Real Environment)

- Decode Base64 payload for further analysis  
- Monitor for repeated encoded executions  
- Correlate with network activity and file events  
- Apply PowerShell execution restrictions (e.g., execution policies, AMSI)  

---

## 🔧 Detection Improvement (Tuning)

To reduce false positives in production environments, detection can be refined as:

```
process.name: "powershell.exe" 
AND process.command_line: "*-enc*" 
AND NOT user.name: "SYSTEM"
```

This tuning helps:

- Exclude legitimate system-level activity  
- Reduce alert noise  
- Improve detection precision  

---

## 🧠 Key Learnings

- Sysmon provides critical visibility into process command-line activity  
- Encoded PowerShell commands are strong indicators of suspicious behavior  
- Behavior-based detection improves detection accuracy  
- Detection tuning is essential for real-world SOC environments  

---

## 📸 Evidence

### Encoded Command Execution

![Encoded Command](../screenshots/investigations/sysmon-encoded-command.png)

---

### Alert Details

![Alert Details](../screenshots/investigations/sysmon-encoded-alert.png)

---

## 📌 Conclusion

This investigation demonstrates how Sysmon enhances visibility into PowerShell activity, enabling accurate detection of obfuscated command execution.

Encoded PowerShell commands represent a high-risk technique and should be closely monitored and tuned for effective detection in enterprise environments.
