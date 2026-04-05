# 🎣 SOC Investigation Report: Email Attachment Phishing Leading to PowerShell Execution (Advanced Attack Chain)

This report documents a detection engineering use case analyzing a multi-stage phishing attack chain where an email attachment leads to PowerShell execution via Microsoft Office applications.

---

## 📌 Summary

A potential phishing attack pattern was analyzed where a malicious email attachment leads to execution of PowerShell through Microsoft Office applications.

This multi-stage attack chain is commonly used by attackers to deliver malware using macro-enabled documents or embedded scripts.

---

## 🖥️ Environment

- **SIEM:** Elastic Stack (Elasticsearch, Kibana, Fleet, Elastic Defend)  
- **Endpoint:** Windows 10 Virtual Machine  
- **User:** kalyan  
- **Host:** desktop-qucd21v  

---

## 🚨 Detection Details

### 🔹 Rule Name:
**Email Attachment → Office → PowerShell Execution Detection**

### 🔹 Detection Logic:

```
process.name: "powershell.exe" 
AND process.parent.name: ("winword.exe" OR "excel.exe") 
AND process.parent.parent.name: "outlook.exe"
```

### 🔹 MITRE ATT&CK Mapping:

- **Tactic:** Initial Access (TA0001)  
- **Technique:** T1566 – Phishing  
- **Tactic:** Execution (TA0002)  
- **Technique:** T1059 – Command and Scripting Interpreter  

---

## 🔍 Investigation Steps

### 1. Log Analysis

Filtered process execution chain using:

```
process.name: "powershell.exe"
```

Reviewed multi-level parent-child relationships.

---

### 2. Key Fields Observed

- **process.name:** powershell.exe  
- **process.parent.name:** winword.exe / excel.exe  
- **process.parent.parent.name:** outlook.exe  
- **user.name:** kalyan  
- **host.name:** desktop-qucd21v  

---

### 3. Behavior Identification

- Outlook launches Office document (Word/Excel)  
- Office application spawns PowerShell  
- Indicates macro execution or embedded script activity  

---

## ⏱️ Attack Timeline (Expected)

```
1. User receives phishing email in Outlook  
2. User opens malicious attachment (Word/Excel)  
3. Macro or embedded script executes  
4. Office application launches PowerShell  
5. PowerShell executes payload or downloads malware  
```

---

## 🧠 Behavioral Analysis

### 🔹 Observed Behavior (Conceptual)

```
outlook.exe → winword.exe → powershell.exe
```

### 🔹 Interpretation

- Office applications do not normally spawn PowerShell  
- When triggered via Outlook, it strongly indicates phishing  
- Likely involves macro-enabled or weaponized document  

This is considered a high-confidence malicious execution chain.

---

## ⚖️ Analysis & Findings

### 🔹 Indicators

- Multi-level parent-child process chain  
- Office spawning PowerShell  
- Email client acting as initial vector  

### 🔹 Context Evaluation

- Not fully reproducible in lab environment  
- Detection based on real-world attacker techniques  
- Behavior aligns with known phishing attack patterns  

---

## 🧭 MITRE ATT&CK Mapping

- T1566 – Phishing  
- T1059 – Command and Scripting Interpreter  

---

## 🧾 Final Classification

```
Malicious Activity → Phishing Attack Execution Chain
```

---

## 🚀 SOC Analyst Decision

- **Severity:** High  
- **Action Taken:** Immediate investigation required  

### 🔹 Recommended Actions (Real Environment)

- Isolate affected endpoint  
- Block malicious email sender/domain  
- Analyze attachment file for malicious content  
- Review PowerShell command execution (`process.command_line`)  
- Perform full endpoint scan and threat hunting  

---

## 🧠 Key Learnings

- Phishing attacks often involve multi-stage execution chains  
- Parent-child relationships provide critical detection visibility  
- Office → PowerShell is a strong indicator of compromise  
- Outlook as initial parent confirms phishing vector  
- Detection engineering must incorporate real-world attack patterns  

---

## 📸 Evidence

### Expected Attack Chain

![Attack Chain](../screenshots/investigations/email-phishing-chain.png)

---

### Detection Logic

![Detection Rule](../screenshots/investigations/email-phishing-rule.png)

---

## 📌 Conclusion

This case demonstrates how email-based phishing attacks can lead to PowerShell execution through Office applications.

By analyzing multi-level process relationships, SOC analysts can detect complex attack chains and respond effectively to real-world threats.
