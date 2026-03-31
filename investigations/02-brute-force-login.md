# 🛡️ SOC Investigation Report: Brute Force Login Attempt Detection

This report documents a simulated SOC investigation identifying potential brute force activity using authentication logs in an Elastic Stack lab environment.

---

## 📌 Summary

A potential brute force attack was detected based on multiple failed login attempts (Event ID 4625) targeting a single user account within a short time window. The activity was identified using a threshold-based detection rule in Elastic SIEM.

---

## 🖥️ Environment

- **SIEM:** Elastic Stack (Elasticsearch, Kibana, Fleet, Elastic Defend)
- **Endpoint:** Windows 10 Virtual Machine
- **User:** kalyan
- **Host:** desktop-qucd21v

---

## 🚨 Detection Details

### 🔹 Rule Name:
**Brute Force Login Detection**

### 🔹 Detection Logic:

```
event.code: 4625 and event.category: authentication
```

### 🔹 Threshold Configuration:

```
Group by: user.name  
Threshold: ≥ 5 attempts  
Time window: 5 minutes
```

---

## 🔍 Investigation Steps

### 1. Log Analysis

Filtered authentication logs using:

```
event.code: 4625
```

Observed multiple failed login attempts.

---

### 2. Key Fields Identified

- **user.name:** kalyan
- **host.name:** desktop-qucd21v
- **event.outcome:** failure
- **event.code:** 4625

---

### 3. Pattern Identification

- Total failed attempts: **5+**
- Time window: **~2 minutes**
- Same user targeted repeatedly

---

## 🧠 Behavioral Analysis

### 🔹 Observed Behavior

- Multiple failed login attempts for the same user within a short time frame

### 🔹 Interpretation

- Repeated password guessing activity  
- Consistent with brute force attack pattern  

Brute force attacks are commonly used by attackers to gain unauthorized access by systematically guessing passwords, often targeting exposed services such as RDP or SSH.

---

## ⏱️ Timeline Reconstruction

```
1. User account "kalyan" targeted  
2. Multiple failed login attempts recorded (Event ID 4625)  
3. Attempts occurred within ~2 minutes  
4. Threshold exceeded (≥5 attempts)  
5. Detection rule triggered alert  
```

---

## ⚖️ Analysis & Findings

### 🔹 Indicators of Suspicious Activity

- High frequency of failed login attempts  
- Single user account targeted  
- Short time interval between attempts  

### 🔹 Context Consideration

- Could be user error (forgot password)  
- Could be automated brute force attempt  

---

## 🧭 MITRE ATT&CK Mapping

- T1110 – Brute Force  

---

## 🧾 Final Classification

```
Suspicious Activity → Potential Brute Force Attack Pattern (Requires Validation)
```

---

## 🚀 SOC Analyst Decision

- **Severity:** Medium  
- **Action Taken:** Escalated for further validation  

### 🔹 Recommended Actions:

- Verify with user if login attempts were legitimate  
- Check source of login attempts (local vs remote)  
- Monitor for successful login (Event ID 4624)  
- Investigate for repeated patterns or multiple users targeted  

---

## 🧠 Key Learnings

- Event ID **4625** is critical for detecting failed authentication attempts  
- Threshold-based rules help identify attack patterns  
- Context is required to distinguish false positives from real attacks  
- ECS mapping enables consistent querying (`user.name`, `event.code`)  

---

## 📌 Conclusion

This investigation demonstrates how repeated failed login attempts can be detected and analyzed using Elastic SIEM. By applying threshold-based detection and analyzing authentication logs, SOC analysts can identify potential brute force attacks and take appropriate action.
