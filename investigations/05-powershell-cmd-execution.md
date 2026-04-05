# ⚙️ SOC Investigation Report: Suspicious PowerShell Execution from CMD

This report documents a simulated SOC investigation analyzing suspicious process execution patterns where PowerShell is launched from Command Prompt using Elastic Stack in a controlled lab environment.

---

## 📌 Summary

A suspicious process execution pattern was detected where PowerShell was launched from Command Prompt (cmd.exe). This behavior is commonly associated with script execution and can be leveraged by attackers to run malicious payloads.

---

## 🖥️ Environment

- **SIEM:** Elastic Stack (Elasticsearch, Kibana, Fleet, Elastic Defend)  
- **Endpoint:** Windows 10 Virtual Machine  
- **User:** kalyan  
- **Host:** desktop-qucd21v  

---

## 🚨 Detection Details

### 🔹 Rule Name:
**PowerShell Spawned from CMD Detection**

### 🔹 Detection Logic:

```
process.name: "powershell.exe" AND process.parent.name: "cmd.exe"
```

### 🔹 MITRE ATT&CK Mapping:

- **Tactic:** Execution (TA0002)  
- **Technique:** T1059 – Command and Scripting Interpreter  

---

## 🔍 Investigation Steps

### 1. Log Analysis

Filtered process execution logs using:

```
process.name: "powershell.exe"
```

Observed PowerShell processes initiated from command-line execution.

---

### 2. Key Fields Observed

- **process.name:** powershell.exe  
- **process.parent.name:** cmd.exe  
- **user.name:** kalyan  
- **host.name:** desktop-qucd21v  

---

### 3. Behavior Identification

- PowerShell executed from command prompt  
- Indicates command-line initiated scripting activity  

---

## ⏱️ Timeline Reconstruction

```
1. User "kalyan" opened Command Prompt  
2. Command Prompt launched PowerShell  
3. PowerShell process executed  
4. Detection rule triggered alert  
```

---

## 🧠 Behavioral Analysis

### 🔹 Observed Behavior

```
cmd.exe → powershell.exe
```

### 🔹 Interpretation

- Common attacker technique for executing scripts  
- Also used in legitimate administrative tasks  
- Requires context-based validation  

PowerShell execution from command-line is frequently used by attackers to execute payloads, download scripts, or perform post-exploitation activities.

---

## ⚖️ Analysis & Findings

### 🔹 Indicators

- Parent-child process relationship  
- Command-line initiated execution  

### 🔹 Context Evaluation

- Activity performed manually in lab environment  
- No encoded commands observed  
- No network activity detected  
- No additional suspicious behavior  

---

## 🧭 MITRE ATT&CK Mapping

- T1059 – Command and Scripting Interpreter  

---

## 🧾 Final Classification

```
Suspicious Activity → Requires Context Validation
```

---

## 🚀 SOC Analyst Decision

- **Severity:** Medium  
- **Action Taken:** Monitor, no escalation required  

### 🔹 Recommended Actions (Real Environment)

- Inspect command-line arguments (`process.command_line`)  
- Investigate user activity and intent  
- Correlate with network or file events  
- Monitor for repeated or abnormal behavior  

---

## 🧠 Key Learnings

- Parent-child relationships are critical for detecting attacker behavior  
- PowerShell execution patterns must be monitored closely  
- Not all suspicious behavior is malicious — context is essential  
- Behavior-based detection is more effective than signature-based detection  

---

## 📸 Evidence

### Process Relationship (CMD → PowerShell)

![Process Chain](../screenshots/investigations/powershell-cmd-process.png)

---

### Alert Details

![Alert Details](../screenshots/investigations/powershell-cmd-alert.png)

---

## 📌 Conclusion

This investigation demonstrates how process relationships can be used to detect suspicious activity.

By analyzing parent-child execution patterns and validating context, SOC analysts can identify potential attacker techniques and differentiate them from legitimate administrative actions.
