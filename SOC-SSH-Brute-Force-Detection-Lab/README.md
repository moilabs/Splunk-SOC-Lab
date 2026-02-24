
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

## 🔍 Detection Logic
Detection was implemented using Splunk SPL queries to monitor:

- Multiple failed SSH login attempts per IP

- Top attacking IP addresses

- Logins outside business hours

- Successful SSH logins for correlation
  
![Detection Query](screenshots/03_detection_query.png)

---

## 🚨 Alert Triggered
Splunk alert triggered when brute force threshold exceeded.

![Alert](screenshots/04_SSH_Brute_Force_Alert.png)

---

## 🕵️ Investigation Evidence
- Collected logs provided evidence of attacker IPs and failed login attempts, facilitating incident investigation.

![Logs](screenshots/05_Failed_Password_Logs_&_Attacker_IP.png)

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
