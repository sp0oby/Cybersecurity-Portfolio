# SecureTech Solutions Cybersecurity Portfolio Lab

This repository documents my hands-on cybersecurity analyst portfolio projects, simulated within a controlled home lab environment representing a fictional mid-sized tech company: **SecureTech Solutions**.

SecureTech Solutions is a cloud-based services provider for small businesses, running a modest internal network with web services, databases, and employee workstations. As an entry-level analyst, I built this lab to mimic real-world security challenges: conducting audits, identifying vulnerabilities, hardening systems, setting up monitoring, automating detection, and documenting incidents—all in an ethical, isolated environment.

## Lab Overview & Network Design

The lab consists of three virtual machines running in **VirtualBox** on a Windows 11 host. All VMs communicate over a private **Host-only network** (192.168.56.0/24) for internal simulation, with internet access via NAT or Bridged adapter for updates and tool downloads.

### Virtual Machines & IP Assignments

| VM Name                  | OS                  | Role in SecureTech Solutions                  | Static IP (Host-only) | Internet Access Method | Notes |
|--------------------------|---------------------|-----------------------------------------------|-----------------------|------------------------|-------|
| SecureTech-Server        | Ubuntu Server 24.04 LTS (CLI-only) | Company backend server (web, database)       | 192.168.56.101        | NAT (enp0s3: 10.0.2.15) | Apache, MariaDB, DVWA (vulnerable web app) |
| SecureTech-Workstation   | Windows 10/11       | Employee workstation                          | 192.168.56.102        | NAT                    | Simulated user device |
| Kali-Tools               | Kali Linux (latest) | Security analyst / attacker workstation       | 192.168.56.103        | NAT                    | Nmap, OpenVAS, Wireshark, Burp Suite, etc. |

- **Host-only network range**: 192.168.56.0/24
- **Host IP on the network**: 192.168.56.1 (VirtualBox adapter "Ethernet 2")
- All VMs can ping each other and the host on the 192.168.56.x range.
- Internet access confirmed: `ping 8.8.8.8` works from SecureTech-Server.

### Key Setup Details

1. **VirtualBox Configuration**
   - All VMs use **Host-only Adapter** ("VirtualBox Host-Only Ethernet Adapter") for internal communication.
   - NAT or Bridged adapter added to each VM for internet (primarily on Adapter 1 or 2).
   - DHCP disabled on Host-only network → static IPs assigned manually.

2. **SecureTech-Server (Ubuntu Server)**
   - Installed packages: `apache2`, `mariadb-server`, `php`, `php-mysql`, `git`
   - Deployed **DVWA** (Damn Vulnerable Web Application) at `/var/www/html/dvwa` to simulate a legacy internal web portal with intentional vulnerabilities.
   - DVWA setup: Database `dvwa`, user `dvwa`, password `p@ssw0rd` (lab-only), accessible at http://192.168.56.101/dvwa
   - Permissions fixed: `chmod 777` on `hackable/uploads/` and config directory for exploit simulation.

3. **Tool Locations**
   - Security scanning tools (Nmap, OpenVAS, Wireshark, sqlmap, etc.) → Installed in **Kali-Tools VM**
   - Python (pandas, scapy, etc.) → Used in virtual environments (`python3 -m venv`) on Kali or Server
   - SIEM simulation (ELK Stack / Graylog) → Planned for SecureTech-Server
   - SQL practice → MariaDB on Server + SQLite for scripts

### How This Lab Mimics SecureTech Solutions

- **SecureTech-Server**: Represents the company's production web server and internal database—realistic target for audits and hardening.
- **SecureTech-Workstation**: Simulates an employee machine that could be compromised or used for lateral movement.
- **Kali-Tools**: My "analyst workstation"—used for scanning, exploitation practice, and automation scripting.
- **DVWA deployment**: Models a vulnerable legacy application a small business might still run internally, allowing safe demonstration of common web vulnerabilities (SQLi, XSS, command injection, insecure file upload).

All activities are performed in an isolated lab—no real networks, production systems, or unauthorized access involved.

### Projects in This Portfolio

This lab serves as the foundation for the following documented projects (in progress / upcoming):

1. Security Audit & Vulnerability Scan (Nmap + OpenVAS on DVWA)
2. Network Structure & Traffic Analysis (Wireshark captures)
3. Linux File Permissions Hardening
4. SIEM Dashboard Setup (ELK or Graylog)
5. Python & SQL Automation Scripts (log parsing, threat detection, SQL filters)
6. Incident Response Simulation & Handler’s Journal
7. Additional: Packet Sniffing, Basic Encryption Demo, ML Anomaly Detection

Each project includes code, screenshots, reports, and write-ups showing identification, exploitation (ethical/safe), and mitigation.

### Getting Started / Reproducing the Lab

1. Install VirtualBox + Extension Pack on Windows/Linux host.
2. Create three VMs as described above.
3. Configure Host-only network (DHCP disabled).
4. Assign static IPs (see table).
5. Install Ubuntu Server, Windows, Kali.
6. On Ubuntu Server: Deploy Apache + DVWA as documented.

Feel free to clone and adapt this lab for your own learning.

Happy hunting (ethically)!
