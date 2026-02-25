# SOC SSH Brute Force Detection Lab

## 📌 Project Overview
This lab demonstrates detection of SSH brute force attacks using Splunk SIEM.  
Attack simulation was performed using Hydra and logs were analyzed in Splunk.

---

## 🧩 Lab Architecture
The lab environment consists of:

- Attacker Machine: Kali Linux

- Target Machines: RHEL / Zorin OS

- SIEM Platform: Splunk Enterprise

- Detection: Custom SPL queries monitoring SSH login events
  
![Lab Diagram](screenshots/01_Lab_Diagram.png)

---

## ⚔️ Attack Simulation
SSH brute force attacks were simulated using Hydra to generate multiple failed login attempts against the target machines.

![Hydra Attack](screenshots/02_Hydra_Attack.png)

---

## 🕒 Attack Timeline

SSH brute force simulations were executed from a Kali Linux attacker machine on 12 February 2026.

#### Attack Session 1
- **Start Time:** 2026-02-12 23:24:00
- **Target Host:** 10.236.163.180
- **Target Username:** sadia
- **Tool Used:** Hydra v9.6
- **Wordlist:** rockyou.txt
- **Protocol:** SSH (Port 22)
- **Total Failed Attempts:** 1801

#### Attack Session 2
- **Start Time:** 2026-02-12 23:28:37
- **Target Host:** 10.236.163.53
- **Target Username:** redhat-zb
- **Tool Used:** Hydra v9.6
- **Wordlist:** rockyou.txt
- **Protocol:** SSH (Port 22)
- - **Total Failed Attempts:** 294

Both sessions generated multiple failed SSH authentication attempts, which were successfully detected and logged in Splunk.

No successful login was observed during the attack simulation.

---

## 🗂 MITRE ATT&CK Mapping

This lab maps the SSH brute force simulation to the MITRE ATT&CK framework:

- **Technique ID:** T1110  
- **Technique Name:** Brute Force  
- **Description:** Attempts to gain access by systematically guessing passwords on SSH accounts.  
- **Observed Behavior in Lab:**
  - Multiple failed login attempts from single source IPs
  - Attempts against high-privileged accounts (root, admin)
  - Logins outside normal hours
- **Detection Method:**
  - Splunk SPL queries monitored `/var/log/secure` for failed authentication attempts
  - Alerts configured for multiple failed logins per IP
  - Top attacking IPs visualized on dashboards
    
  ---

## 🔍 Detection Logic

### Time-Based Brute Force Detection

This query detects high-frequency failed SSH login attempts by aggregating events per source IP within a 1-minute window.  
IPs generating more than 5 failed attempts per minute are flagged as potential brute force sources.  
The detection logic supports real-time alerting and rapid identification of suspicious authentication activity.

![Detection Query](screenshots/03_detection_query.png)

---

## 🚨 Alert Triggered
Splunk alert triggered when brute force threshold exceeded.

![Alert](screenshots/04_SSH_Brute_Force_Alert.png)

---

## 🕵️ Investigation Workflow
- Collected logs provided evidence of attacker IPs and failed login attempts, facilitating incident investigation.

![Logs](screenshots/05_Failed_Password_Logs_&_Attacker_IP.png)

---

## 🛡 Mitigation Recommendations  

To reduce the risk of SSH brute-force attacks and strengthen system security, the following measures were implemented:

- Enforced SSH key-based authentication by disabling password authentication.
- Deployed Fail2Ban to automatically block IP addresses after repeated failed login attempts.
- Applied firewall rules to restrict SSH access to trusted IP ranges only.
- Enabled continuous monitoring and real-time alerting through Splunk SIEM.
  
---

## 🛠 Tools Used
- Splunk SIEM
- Kali Linux
- Zorin OS / RHEL 10
- Hydra

---

## 🎯 Skills Demonstrated
- SIEM Monitoring
- Log Analysis
- Brute Force Detection
- Alert Configuration
- SOC Investigation Workflow
