# SecureTech Solutions – Cybersecurity Analyst Portfolio

Welcome! This repository is my **hands-on cybersecurity portfolio** as an aspiring entry-level Cybersecurity Analyst. All projects are built in a fully isolated home lab simulating a mid-sized tech company called **SecureTech Solutions** — a cloud-services provider for small businesses facing common threats like misconfigurations, web vulnerabilities, and insider risks.

Everything here is ethical, self-contained, and documented: scans, exploits (on intentional vulns only), hardening, automation, monitoring, and incident response. No real networks or unauthorized access were involved.

## Lab Environment Overview

I created a realistic small-business network using **VirtualBox** on Windows 11:

- **Network**: Private Host-only (192.168.56.0/24) for VM-to-VM communication  
  Host IP on network: 192.168.56.1  
  Internet via NAT/Bridged adapter on each VM

| VM Name                  | OS                        | Role                              | Static IP (Host-only) | Key Software/Tools Installed                  |
|--------------------------|---------------------------|-----------------------------------|-----------------------|-----------------------------------------------|
| SecureTech-Server        | Ubuntu Server 24.04 LTS (CLI-only) | Backend server (web + DB)        | 192.168.56.101        | Apache2, MariaDB, PHP, DVWA (vulnerable app) |
| SecureTech-Workstation   | Windows 10/11             | Employee endpoint                 | 192.168.56.102        | Browser, basic tools (simulated user device) |
| Kali-Tools               | Kali Linux (latest)       | Analyst / pentest workstation     | 192.168.56.103        | Nmap, OpenVAS/GVM, Wireshark, Burp Suite, sqlmap, Python (pandas, scapy), etc. |

All VMs ping each other successfully. DVWA runs at `http://192.168.56.101/dvwa` (login: admin / password) for safe vulnerability practice.

## Projects Included

Each project folder contains code, screenshots, reports (PDF/Markdown), commands, findings, and lessons learned. Projects build on each other to show a full security lifecycle.

1. **Security Audit & Vulnerability Scan**  
   Nmap service/version/OS fingerprinting + full OpenVAS scan of SecureTech-Server (DVWA target).  
   Identified: open ports (80, 3306), Apache/PHP banners, SQL Injection, XSS, command injection, insecure file upload (CVSS 7.5–9.8).  
   Report: findings table, CVSS scores, small-business remediation advice.

2. **Network Structure & Traffic Analysis**  
   Wireshark captures between VMs, topology diagram (Draw.io), analysis of insecure protocols and potential lateral movement paths.

3. **Linux File Permissions Hardening**  
   Bash scripts and commands (`chmod`, `chown`) to secure files/folders on Ubuntu server post-audit.

4. **SIEM Dashboard Setup**  
   ELK Stack (or Graylog) on SecureTech-Server ingesting logs from Apache/DVWA. Custom dashboards and alerts for anomalies.

5. **Python & SQL Automation Scripts**  
   Scripts for log parsing (text files + regex), SQL threat filtering (`SELECT ... WHERE attempts > 5`), anomaly detection.  
   Used virtual environments (`venv`) to comply with modern packaging rules.

6. **Incident Response Simulation & Handler’s Journal**  
   Simulated phishing/data breach using DVWA vulns. NIST-based response playbook + timestamped journal (detection → containment → recovery).

7. **Additional Demonstrations**  
   - Packet sniffing with Scapy  
   - Basic encryption/keylogger detection demo  
   - (Planned) ML-based anomaly detection on logs

## Skills Demonstrated

- Vulnerability scanning & reporting (Nmap, OpenVAS/GVM)  
- Web application security (DVWA exploits: SQLi, XSS, command injection, file upload)  
- Linux administration & hardening  
- Network traffic analysis (Wireshark)  
- SIEM configuration & log monitoring  
- Scripting & automation (Python, Bash, SQL)  
- Incident response documentation (NIST framework)  
- Ethical hacking mindset in controlled lab

## Tools & Technologies Used

- **Scanning**: Nmap, OpenVAS/GVM, Nikto  
- **Analysis**: Wireshark, tcpdump  
- **Web/App Sec**: DVWA, Burp Suite, sqlmap  
- **Scripting**: Python (pandas, scapy), Bash  
- **Database**: MariaDB, SQLite  
- **SIEM**: ELK Stack / Graylog  
- **Lab**: VirtualBox, Ubuntu Server, Kali Linux, Windows

## How to Navigate This Repo

- `/projects/` – One folder per project with READMEs, code, screenshots, reports  
- `/lab-setup/` – VM configs, network diagrams, installation notes  
- `/reports/` – Consolidated PDFs (audit reports, incident journals)  
- `/scripts/` – All automation code (with venv instructions)

## Contact & Next Steps

I'm actively seeking entry-level Cybersecurity Analyst / SOC Analyst roles.  
Feel free to reach out!  

- X / Twitter: 
- Email:  
- LinkedIn: 

Thanks for visiting — happy to discuss any project in detail during interviews!

Last updated: January 2026
