# 🧪 Blue Team Detection Lab – Reconnaissance & Exfiltration Tool Monitoring

## 📖 Overview

In this cybersecurity lab, I focused on detecting early-stage attacker activity by monitoring for the execution of **reconnaissance** and **credential access tools** often used in real-world breaches. The goal was to simulate how attackers operate in the initial phases of an attack and build **Blue Team detections** using **Wazuh** and **Sysmon**. 

*Refrence Wazuh-Siem Repository for SIEM setup*.

To achieve this, I created custom Wazuh rules that monitor **Sysmon Event ID 1 (Process Creation)** for suspicious process names commonly associated with attacker activity, including:

- `whoami.exe` – user enumeration  
- `systeminfo.exe` – system reconnaissance  
- `netstat.exe` – network connection discovery  
- `cmd.exe`, `powershell.exe` – command execution  
- `mimikatz.exe` / `mimi.exe` – credential dumping  
- `nmap.exe` – network scanning  
- `nc.exe` (netcat) – data exfiltration or reverse shell  
- `procdump.exe` – dumping LSASS memory

This lab showcases how defenders can catch malicious activity **early in the attack chain**, by identifying the use of tools that don’t typically appear in normal user behavior.

---

## 🎯 Objectives

- Detect suspicious process creation using Sysmon logs.
- Create custom Wazuh rules to trigger alerts on specific tools.
- Understand how attackers use legitimate tools to evade detection.
- Simulate realistic adversary behavior in a safe lab environment.
- Improve detection and alerting capabilities for common threat techniques.

---

## 🔍 Why This Matters in Cybersecurity

Attackers rarely start with malware. Instead, they often use **built-in or widely available tools** during the **reconnaissance** and **credential access** phases of the cyber kill chain.

For example:
- `whoami` and `systeminfo` help determine the user's privileges and environment.
- `mimikatz` can extract passwords and tokens from memory.
- `netstat`, `nmap`, and `arp` help identify lateral movement targets.
- `nc.exe` or `powershell` can be used to exfiltrate data or establish command and control (C2).

By detecting these tools early, defenders can interrupt the attack **before exploitation or data loss occurs**.

---

## 🧰 Tools & Technologies Used

- **Wazuh** – for log collection, rule matching, and alerting
- **Sysmon** – for detailed endpoint telemetry (especially process creation)
- **Kibana** – for visualization and analysis of alerts
- **Windows 11 VM** – target endpoint with Sysmon and Wazuh agent installed
- **Custom Rules** – written in `local_rules.xml` to detect suspicious binaries

---

## 🛠 Custom Wazuh Rule Example
Below is the rule I created and tested

![image alt](https://github.com/UVSasa/Network-Defense/blob/main/Screenshots/WhoamiRule.png?raw=true)

Now when I ran the command whoami from the command prompt or from powershell I received the alert below. Notice the description I put in the rule is what shows up in the logs.

![image alt](<img width="1219" height="688" alt="Whoamilog" src="https://github.com/user-attachments/assets/b6cda3b6-12b7-4b3f-bd14-29e2e7355e89" />)



