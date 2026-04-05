# 🌐 SOC Investigation Report: Suspicious PowerShell Network Activity

This report documents a simulated SOC investigation identifying PowerShell-based network activity using Elastic Stack in a controlled lab environment.

---

## 📌 Summary

A network connection initiated by PowerShell was detected using Elastic SIEM. The activity involved outbound communication over HTTP (port 80), which may indicate web requests, payload downloads, or command-and-control (C2) behavior.

The alert was generated using a behavior-based detection rule and analyzed to determine whether the activity was malicious or benign.

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
process.name: "powershell.exe" AND event.category: network AND network.destination.port: (80 OR 443)
```

### 🔹 MITRE ATT&CK Mapping:

- **Tactic:** Command and Control (TA0011)  
- **Technique:** T1071 – Application Layer Protocol  

---

## 🔍 Investigation Steps

### 1. Log Analysis

Filtered network activity using:

```
process.name: "powershell.exe" AND event.category: network
```

Observed PowerShell initiating outbound network communication.

---

### 2. Key Fields Observed

- **process.name:** powershell.exe  
- **user.name:** kalyan  
- **host.name:** desktop-qucd21v  
- **destination.port:** 80  
- **network.protocol:** tcp / http  
- **dns.resolved_ip:** external IP  

---

### 3. Event Correlation

- DNS resolution (port 53) observed prior to connection  
- Followed by outbound HTTP request (port 80)  
- All events linked to the same process (`powershell.exe`)  

---

## ⏱️ Timeline Reconstruction

```
1. PowerShell process executed by user "kalyan"  
2. DNS query performed (port 53)  
3. Domain resolved to external IP  
4. HTTP connection initiated (port 80)  
5. Detection rule triggered alert  
```

---

## 🧠 Behavioral Analysis

### 🔹 Observed Behavior

- PowerShell initiating outbound network communication  

### 🔹 Interpretation

- Legitimate web request (e.g., Invoke-WebRequest)  
- Script downloading external resources  
- Potential command-and-control (C2) communication  

PowerShell network activity is commonly used by attackers for payload delivery or C2 communication, making it an important behavior to monitor.

---

## ⚖️ Analysis & Findings

### 🔹 Indicators

- PowerShell used for network communication  
- External IP connection over HTTP  
- Behavior aligns with common attacker techniques  

### 🔹 Context Evaluation

- Activity executed in controlled lab environment  
- Command used: `Invoke-WebRequest`  
- Domain accessed: `example.com` (known benign)  

---

## 🧭 MITRE ATT&CK Mapping

- T1071 – Application Layer Protocol  

---

## 🧾 Final Classification

```
Benign Activity → Expected Behavior in Controlled Lab Environment
```

---

## 🚀 SOC Analyst Decision

- **Severity:** Low  
- **Action Taken:** No escalation required  

### 🔹 Recommended Actions (Real Environment)

- Verify domain reputation  
- Monitor frequency of connections  
- Check for encoded or obfuscated PowerShell commands  
- Correlate with additional suspicious behavior

---

## 🧠 Key Learnings

- PowerShell network activity must be closely monitored  
- DNS (port 53) and HTTP/HTTPS (80/443) events are part of the same flow  
- Not all alerts indicate malicious behavior — context validation is essential  
- Detection tuning improves accuracy and reduces false positives  

---

## 📸 Evidence

### Network Activity Logs

![Network Logs](../screenshots/investigations/powershell-network-logs.png)

---

### Analyzer Graph

![Analyzer Graph](../screenshots/investigations/powershell-network-analyzer.png)

---

### Alert Details

![Alert Details](../screenshots/investigations/powershell-network-alert.png)

---

## 📌 Conclusion

This investigation demonstrates how PowerShell-based network activity can be detected and analyzed using Elastic SIEM.

By correlating DNS and HTTP events and validating execution context, SOC analysts can distinguish between legitimate and potentially malicious behavior.
