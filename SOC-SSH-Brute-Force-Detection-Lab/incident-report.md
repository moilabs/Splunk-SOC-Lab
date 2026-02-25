# 🔐 Security Incident Report  
## SSH Brute Force Attack Detection – SOC Lab Case Study  

---

## 1️⃣ Incident Summary  

On 12 February 2026, a simulated SSH brute-force attack was detected against Linux endpoints within the lab environment.  

The attack involved multiple failed authentication attempts originating from a single external source IP and targeting user accounts over SSH (Port 22).

The activity was successfully detected through Splunk SIEM using custom time-based detection logic.

---

## 2️⃣ Detection Details  

**Detection Method:**  
Custom SPL query aggregating failed SSH login attempts per IP within a 1-minute time window.

**Trigger Condition:**  
More than 5 failed login attempts per source IP within 60 seconds.

**Log Source:**  
/var/log/secure  

**SIEM Platform:**  
Splunk Enterprise  

The alert was automatically triggered when the defined brute-force threshold was exceeded.

---

## 3️⃣ Timeline of Events  

### Attack Session 1  
- **Start Time:** 2026-02-12 23:24:00  
- **Target Host:** 10.236.163.180  
- **Target Username:** sadia  
- **Total Failed Attempts:** 1801  

### Attack Session 2  
- **Start Time:** 2026-02-12 23:28:37  
- **Target Host:** 10.236.163.53  
- **Target Username:** redhat-zb  
- **Total Failed Attempts:** 294  

Both sessions generated abnormal authentication activity and triggered SOC alerting mechanisms.

---

## 4️⃣ Indicators of Compromise (IOCs)  

- Repeated failed SSH login attempts  
- High-volume authentication attempts within short time intervals  
- Multiple attempts targeting privileged accounts  
- Source IP generating more than 5 failed attempts per minute  

---

## 5️⃣ MITRE ATT&CK Classification  

- **Technique ID:** T1110  
- **Technique Name:** Brute Force  
- **Tactic:** Credential Access  

The observed behavior aligns with brute-force password guessing against SSH services.

---

## 6️⃣ Investigation Findings  

The SOC investigation confirmed:

- No successful authentication occurred  
- No unauthorized access was achieved  
- Attack activity was limited to failed login attempts  
- No lateral movement or persistence behavior observed  

Log correlation and time-based aggregation validated detection accuracy.

---

## 7️⃣ Impact Assessment  

- **Data Exposure:** None  
- **System Compromise:** Not observed  
- **Business Impact:** Minimal (Lab Simulation)  
- **Risk Level:** Medium (Credential Access Attempt)  

---

## 8️⃣ Response Actions Taken  

- Alert acknowledged and reviewed  
- Source IP activity analyzed  
- Authentication logs validated  
- No containment required (simulated lab environment)  

---

## 9️⃣ Mitigation & Hardening Measures  

- Disabled SSH password authentication (key-based access enforced)  
- Implemented Fail2Ban for automated IP blocking  
- Restricted SSH access via firewall rules  
- Enabled continuous SIEM monitoring and alerting  

---

## 🔟 Lessons Learned  

- Time-based aggregation effectively detects brute-force attempts  
- Real-time alerting significantly reduces detection delay  
- Proper log monitoring is critical for early credential attack detection  
- MITRE mapping improves structured threat classification  

---
