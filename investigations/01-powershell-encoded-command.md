# 🛡️ SOC Investigation Report: Suspicious PowerShell Encoded Execution

This report documents a simulated SOC investigation conducted in a controlled Elastic Stack lab environment. It demonstrates alert triage, log analysis, and investigation workflow for suspicious PowerShell activity.

---

## 📌 Summary

A suspicious PowerShell execution was detected involving an encoded command using the `-enc` flag. The activity was analyzed using Elastic Stack (ELK), and investigation revealed behavior consistent with obfuscated script execution and potential malicious intent.

---

## 🖥️ Environment

* **SIEM:** Elastic Stack (Elasticsearch, Kibana, Fleet, Elastic Defend)
* **Endpoint:** Windows 10 Virtual Machine
* **User:** kalyan
* **Host:** desktop-qucd21v

---

## 🚨 Detection Details

### 🔹 Alert 1:

**Rule Name:** Suspicious PowerShell Encoded Command  
**Detection Logic:**

```
process.name: "powershell.exe" AND process.args: "-enc"
```

### 🔹 Alert 2:

**Rule Name:** Suspicious PowerShell Script Execution (4104)  
**Detection Logic:**  
Detection of PowerShell Script Block Logging containing suspicious keywords such as:

- Invoke-Expression (IEX)  
- DownloadString  

---

## 🔍 Investigation Steps

### 1. Process Analysis

- **Process:** powershell.exe  
- **Parent Process:** powershell.exe  
- **User:** kalyan  

**Command Executed:**

```
powershell.exe -enc SQBFAFgAIAAoAE4AZQB3AC0ATwBiAGoAZQBjAHQAIABOAGUAdAAuAFcAZQBiAEMAbABpAGUAbgB0ACkA
```

---

### 2. Decoding the Command

The Base64 encoded command was decoded using PowerShell/CyberChef.

**Decoded Output:**

```
IEX (New-Object Net.WebClient)
```

---

### 3. Behavioral Analysis

#### 🔹 Process Behavior

- PowerShell executed with encoded command  
- Indicates obfuscation attempt  

#### 🔹 File Activity

- Temporary files created and deleted:

```
C:\Users\kalyan\AppData\Local\Temp\__PSScriptPolicyTest_*
```

- Indicates script execution and execution policy checks  

#### 🔹 Library Activity

- Multiple DLLs loaded during execution  
- Normal behavior for process execution  

#### 🔹 Network Activity

- No outbound network connections observed  
- Indicates no payload download occurred in this instance  

---

### 4. Timeline Reconstruction

```
1. PowerShell process started  
2. Encoded command executed (-enc)  
3. Script activity triggered (temporary file creation/deletion)  
4. Libraries loaded during execution  
5. Process terminated  
```

---

## 🧠 Analysis & Findings

### 🔹 Indicators of Suspicious Behavior

- Use of `-enc` (Base64 encoding)  
- Presence of `Invoke-Expression (IEX)`  
- Use of `Net.WebClient`  

Use of `Net.WebClient` is commonly associated with downloading payloads from attacker-controlled servers during initial access or post-exploitation phases.

From an analyst perspective, the combination of encoded PowerShell execution and IEX usage significantly increases the likelihood of malicious intent, even in the absence of network activity.

### 🔹 Context Evaluation

- Activity performed in controlled lab environment  
- No external network communication observed  
- No persistence mechanisms detected  

---

## 🧭 MITRE ATT&CK Mapping

- T1059.001 – PowerShell  
- T1027 – Obfuscated/Encoded Files or Information  
- T1105 – Ingress Tool Transfer (potential via WebClient)  

---

## ⚖️ Final Classification

```
Suspicious Behavior → Malicious Execution Pattern (Validated in Controlled Lab Environment)
```

---

## 🚀 SOC Analyst Decision

- **Severity:** High  
- **Action Taken:** Escalated to Tier 2 / Incident Response team  

**Recommended Actions:**

- Decode and analyze full payload  
- Check for persistence mechanisms  
- Investigate lateral movement  
- Monitor for repeated behavior  

---

## 🧠 Key Learnings

- Detection requires both behavior-based and content-based analysis  
- Encoded PowerShell commands are strong indicators but require context  
- Process correlation using `process.entity_id` is critical  
- Not all suspicious behavior is malicious — validation is essential  

---

## 📌 Conclusion

This investigation demonstrates how SOC analysts detect, analyze, and validate suspicious PowerShell activity using Elastic SIEM. By correlating alerts, decoding payloads, and reconstructing process behavior, analysts can accurately determine threat intent and respond effectively.
