# 🎣 SOC Investigation Report: Suspicious Browser-Spawning PowerShell Activity (Phishing Execution Pattern)

This report documents a detection engineering use case analyzing abnormal process relationships where a web browser spawns PowerShell, a pattern commonly associated with phishing and malicious script execution.

---

## 📌 Summary

A high-risk execution pattern was identified where a web browser spawns PowerShell. This behavior is strongly associated with phishing attacks and malicious script execution.

Although not triggered in the lab environment, this detection is based on real-world attacker techniques and is critical for identifying initial access and execution stages.

---

## 🖥️ Environment

- **SIEM:** Elastic Stack (Elasticsearch, Kibana, Fleet, Elastic Defend)  
- **Endpoint:** Windows 10 Virtual Machine  
- **User:** kalyan  
- **Host:** desktop-qucd21v  

---

## 🚨 Detection Details

### 🔹 Rule Name:
**Browser Spawning PowerShell Detection**

### 🔹 Detection Logic:

```
process.name: "powershell.exe" AND process.parent.name: ("msedge.exe" OR "chrome.exe")
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

Reviewed parent-child process relationships.

---

### 2. Key Fields Observed

- **process.name:** powershell.exe  
- **process.parent.name:** explorer.exe (lab observation)  
- **user.name:** kalyan  
- **host.name:** desktop-qucd21v  

---

### 3. Behavior Validation

- No instances of browser spawning PowerShell observed in lab  
- PowerShell executions were initiated manually (parent: explorer.exe)  
- Detection logic validated against expected attacker behavior  

---

## ⏱️ Expected Attack Timeline (Real-World Scenario)

```
1. User clicks phishing link in browser  
2. Malicious script executes within browser context  
3. Browser spawns PowerShell process  
4. PowerShell executes malicious payload  
5. System compromise initiated  
```

---

## 🧠 Behavioral Analysis

### 🔹 Observed Behavior (Lab)

```
explorer.exe → powershell.exe
```

### 🔹 Expected Malicious Behavior

```
browser.exe → powershell.exe
```

### 🔹 Interpretation

- Browsers do not normally spawn PowerShell processes  
- Such behavior strongly indicates:

  - Phishing attack execution  
  - Malicious script or exploit activity  
  - Payload delivery via browser  

This makes the detection a high-confidence indicator of compromise in real-world environments.

---

## ⚖️ Analysis & Findings

### 🔹 Indicators

- Abnormal parent-child process relationship  
- PowerShell execution from browser context  

### 🔹 Context Evaluation

- No malicious behavior triggered in lab  
- Detection created based on known attacker techniques  
- Behavior validated using expected normal vs abnormal patterns  

---

## 🧭 MITRE ATT&CK Mapping

- T1059 – Command and Scripting Interpreter  

---

## 🧾 Final Classification

```
High-Risk Suspicious Behavior → Phishing Execution Pattern
```

---

## 🚀 SOC Analyst Decision

- **Severity:** High  
- **Action Taken:** Detection rule created and monitored  

### 🔹 Recommended Actions (Real Environment)

- Immediately isolate affected host  
- Investigate PowerShell command-line activity (`process.command_line`)  
- Check for downloaded payloads or scripts  
- Correlate with network and file activity  
- Perform threat hunting across endpoints  

---

## 🧠 Key Learnings

- Parent-child process relationships are critical for detecting phishing execution  
- Not all attack behaviors can be easily simulated in lab environments  
- Detection engineering must include real-world threat intelligence  
- Browser spawning PowerShell is a high-confidence IOC  

---

## 📸 Evidence

### Expected Malicious Process Chain

![Process Chain](../screenshots/investigations/browser-powershell-pattern.png)

---

### Detection Rule Logic

![Detection Rule](../screenshots/investigations/browser-powershell-rule.png)

---

## 📌 Conclusion

This case demonstrates the importance of detecting abnormal process relationships in identifying phishing attacks.

Even without direct lab simulation, understanding attacker behavior and building proactive detections enables SOC analysts to identify and respond to threats effectively.
