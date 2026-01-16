# Project 2: Analyzing Network Structure and Security

This folder contains documentation, diagrams, packet captures, and analysis for **Project 2** of my cybersecurity portfolio.

As part of the **SecureTech Solutions** simulation, this project maps the lab network topology, captures and analyzes live traffic between VMs, identifies structural and security risks (e.g., flat network allowing lateral movement, clear-text credential transmission), and provides recommendations for improvement.

## Project Overview

- **Objective**  
  Create a network diagram of the SecureTech lab, capture live traffic between VMs, analyze for insecure protocols/clear-text data/lateral movement risks, and recommend mitigations suitable for a small-business environment.

- **Company Context**  
  SecureTech Solutions operates a flat, single-subnet internal network with a central server and employee workstations. Project 1 audit revealed an exposed web service on port 80. This project examines whether the network structure allows easy lateral movement or exposes sensitive data in transit.

- **Skills Demonstrated**  
  - Network topology mapping  
  - Packet capture and analysis  
  - Identification of insecure protocols and risks  
  - Security recommendation and mitigation planning

- **Tools Used**  
  - Draw.io (diagramming)  
  - Wireshark (packet capture and analysis)  
  - Simulated traffic generation (ping, FTP, Telnet, HTTP Basic Auth)

- **Key Findings Summary**  
  (To be filled after analysis)  
  Flat network with no segmentation allows lateral movement from compromised workstation to server. Clear-text credentials transmitted via FTP/Telnet/HTTP Basic Auth. Recommend VLANs/firewall rules and secure protocols.

## Lab Setup Additions for Demonstration

To make Wireshark captures more illustrative of real-world security issues, the following **intentionally insecure services** were temporarily enabled on SecureTech-Server (192.168.56.101). These are **lab-only** and will be disabled after the project.

1. **FTP (vsftpd)** – Clear-text username/password transmission  
   - Installed: `sudo apt install vsftpd -y`  
   - Test user: `ftpuser` (created with password)  
   - Purpose: Capture plain-text FTP login in Wireshark

2. **Telnet (telnetd)** – All session data unencrypted  
   - Installed: `sudo apt install telnetd -y`  
   - Purpose: Capture full session (including password) in clear text

3. **HTTP Basic Auth test directory** – Credentials base64-encoded (not encrypted)  
   - Directory: `/var/www/html/test-auth`  
   - .htpasswd created with `htpasswd -c /etc/apache2/.htpasswd testuser`  
   - Apache config: Added `<Directory>` block with Basic Auth  
   - Purpose: Capture Authorization header with base64(user:pass)

All additions are **reversible**:
- `sudo systemctl disable --now vsftpd`
- `sudo apt purge telnetd`
- Remove auth config from `/etc/apache2/sites-available/000-default.conf`

## Files in This Folder

- `network-diagram.drawio` / `network-diagram.png` — Visual topology of VMs, IPs, and connections
- `wireshark-capture.pcapng` — Raw packet capture file(s)
- `analysis-report.md` — Full write-up with screenshots, findings, and recommendations
- `screenshots/` — Images of Wireshark filters, packet details, clear-text credentials, etc.

## Setup Notes

- **Network**: Private Host-only (192.168.56.0/24)  
  - SecureTech-Server: 192.168.56.101  
  - SecureTech-Workstation: 192.168.56.102  
  - Kali-Tools: 192.168.56.103  
  - Host: 192.168.56.1

- **Performed from**: Kali-Tools VM (primary capture point) and Windows host (optional Wireshark)

## Lessons Learned

- Flat networks are common in small businesses but enable easy lateral movement after initial compromise.
- Unencrypted protocols (FTP, Telnet, HTTP Basic Auth) remain a significant risk even in modern environments.
- Wireshark is essential for validating audit findings and demonstrating real traffic risks.

For full portfolio context, see the main repo [README](../../README.md).
