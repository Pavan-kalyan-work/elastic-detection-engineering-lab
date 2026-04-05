# 🎣 SOC Investigation Report: Suspicious PowerShell-Based File Download (Phishing Simulation)

This report documents a simulated SOC investigation analyzing PowerShell-based network activity associated with potential phishing behavior using Elastic Stack in a controlled lab environment.

---

## 📌 Summary

A suspicious network activity was detected where PowerShell initiated an outbound HTTP connection to an external IP address. This behavior is commonly associated with phishing attacks, where a user executes a script that downloads a payload from the internet.

---

## 🖥️ Environment

- **SIEM:** Elastic Stack (Elasticsearch, Kibana, Fleet, Elastic Defend)  
- **Endpoint:** Windows 10 Virtual Machine  
- **User:** kalyan  
- **Host:** desktop-qucd21v  

---

## 🚨 Detection Details

### 🔹 Rule Name:
**PowerShell Network Connection Detection**

### 🔹 Detection Logic:

```
process.name: "powershell.exe" AND event.category: "network" AND destination.port: (80 OR 443)
```

### 🔹 MITRE ATT&CK Mapping:

- **Tactic:** Command and Control (TA0011)  
- **Technique:** T1071 – Application Layer Protocol  

---

## 🔍 Investigation Steps

### 1. Log Analysis

Filtered PowerShell network activity using:

```
process.name: "powershell.exe" AND event.category: "network"
```

Observed PowerShell initiating outbound network connections.

---

### 2. Key Fields Observed

- **process.name:** powershell.exe  
- **user.name:** kalyan  
- **host.name:** desktop-qucd21v  
- **destination.address:** 104.18.27.120  
- **destination.port:** 80  
- **network.protocol:** http  

---

### 3. Behavior Identification

- PowerShell executed by user  
- Outbound HTTP connection initiated  
- External IP contacted  

---

## ⏱️ Timeline Reconstruction

```
1. User "kalyan" executed PowerShell  
2. PowerShell initiated outbound network request  
3. External server responded (IP: 104.18.27.120)  
4. Detection rule triggered alert  
```

---

## 🧠 Behavioral Analysis

### 🔹 Observed Behavior

```
PowerShell → External HTTP connection
```

### 🔹 Interpretation

- Commonly observed in phishing attacks  
- Used for malicious script downloads  
- Potential command-and-control (C2) communication  

PowerShell is frequently abused by attackers to download payloads or execute remote scripts, making this behavior highly relevant for SOC monitoring.

---

## ⚖️ Analysis & Findings

### 🔹 Indicators

- PowerShell used for network communication  
- External IP connection over HTTP  
- User-initiated execution  

### 🔹 Context Evaluation

- Activity simulated in controlled lab environment  
- Known benign domain (`example.com`) used  
- No additional malicious indicators observed  

---

## 🧭 MITRE ATT&CK Mapping

- T1071 – Application Layer Protocol  

---

## 🧾 Final Classification

```
Suspicious Activity → Requires Context Validation
```

---

## 🚀 SOC Analyst Decision

- **Severity:** Low to Medium  
- **Action Taken:** Monitor activity, no escalation required  

### 🔹 Recommended Actions (Real Environment)

- Validate domain and IP reputation  
- Monitor for repeated or automated behavior  
- Enable PowerShell Script Block Logging (Event ID 4104)  
- Correlate with process, file, and network events  

---

## 🧠 Key Learnings

- PowerShell is frequently abused in phishing attacks  
- Network-based detection can reveal suspicious behavior without full command visibility  
- Detection tuning is required to reduce false positives  
- Lack of command-line logging limits investigation depth  

---

## 📸 Evidence

### Network Activity

![Network Activity](../screenshots/investigations/powershell-phishing-network.png)

---

### Alert Details

![Alert Details](../screenshots/investigations/powershell-phishing-alert.png)

---

## 📌 Conclusion

This investigation demonstrates how PowerShell-based network activity can indicate potential phishing behavior.

Even without full command-line visibility, correlating process and network telemetry enables SOC analysts to identify suspicious activity and make informed decisions.
