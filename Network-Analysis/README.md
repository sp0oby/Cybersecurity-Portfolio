# Project 2: Analyzing Network Structure and Security

This project maps the SecureTech Solutions lab network, captures live traffic between VMs, analyzes for structural flaws and modern security risks (e.g., weak encryption, unencrypted IoT protocols, vulnerable remote access), and provides realistic mitigations for a small-business environment.

## Project Overview

- **Objective**  
  Diagram the lab topology, capture and dissect traffic to identify insecure configurations, lateral movement risks, and protocol weaknesses, then recommend current best-practice fixes.

- **Company Context**  
  SecureTech Solutions uses a flat, single-subnet internal network (192.168.56.0/24) with a central backend server and employee workstations. Project 1 audit exposed service banners and application flaws. This project evaluates whether the network structure amplifies those risks (e.g., unencrypted remote access or IoT traffic).

- **Skills Demonstrated**  
  - Network topology visualization  
  - Packet-level traffic capture & analysis (Wireshark)  
  - Identification of 2025–2026 relevant risks (weak TLS, unencrypted protocols, VPN misconfigs)  
  - Practical mitigation planning for small businesses

- **Tools Used**  
  - Draw.io (diagramming)  
  - Wireshark (capture & analysis)  
  - OpenVPN (weak VPN demo)  
  - Mosquitto (unencrypted MQTT demo)  
  - Apache + weak TLS config (HTTP3/TLS issues demo)

- **Key Findings Summary** (to be filled after analysis)  
  Flat network enables lateral movement. Weak TLS ciphers, unencrypted MQTT, and misconfigured VPN expose data/handshakes. Recommend segmentation, TLS 1.3 only, and encrypted protocols.

## Lab Setup Additions (Modern Vulnerabilities for Testing)

To simulate current (2025–2026) risks visible in Wireshark, the following were intentionally configured on SecureTech-Server (192.168.56.101). All are **lab-only** and reversible.

1. **Misconfigured OpenVPN (Weak Ciphers)**  
   - Simulates CVE-2025-20333 style remote access flaws (weak negotiation, potential RCE/lateral movement)  
   - Config: AES-128-CBC (outdated/weak) on UDP 1194  
   - Purpose: Capture weak cipher handshake

2. **Unencrypted MQTT Broker (Mosquitto)**  
   - Simulates 2026 IoT risks (clear-text device messages)  
   - Port: 1883 (no TLS)  
   - Purpose: Capture plain-text publish/subscribe messages

3. **Weak TLS/HTTP3 Server (Apache)**  
   - Simulates HTTP3/QUIC issues (weak ciphers, fallback risks)  
   - Config: Added deprecated ciphers (e.g., RC4) to SSL suite  
   - Purpose: Capture weak cipher negotiation and unencrypted fallback

**Reversal Commands** (run after project):
- `sudo systemctl disable --now openvpn@server; sudo apt purge openvpn -y`
- `sudo systemctl disable --now mosquitto; sudo apt purge mosquitto -y`
- Restore Apache SSL config & restart: `sudo systemctl restart apache2`

## Files in This Folder

- `network-diagram.drawio` / `network-diagram.png` — Topology of VMs, IPs, and added services
- `wireshark-capture.pcapng` — Raw traffic captures (insecure logins, MQTT, VPN, weak TLS)
- `analysis-report.md` — Detailed write-up with screenshots, findings, and recommendations
- `screenshots/` — Wireshark filters, weak cipher handshakes, clear-text MQTT, etc.

## Setup Notes

- **Network**: Private Host-only (192.168.56.0/24)  
  - SecureTech-Server: 192.168.56.101  
  - SecureTech-Workstation: 192.168.56.102  
  - Kali-Tools: 192.168.56.103  
  - Host: 192.168.56.1

- **Capture Interface on Kali**: eth1 / enp0s8 (address 192.168.56.103)

- **Performed from**: Kali-Tools VM (primary capture) and Workstation (traffic generation)

## Lessons Learned

- Flat networks remain common in small businesses but drastically increase lateral movement risk.
- Weak/outdated encryption (e.g., AES-128-CBC, RC4) and unencrypted protocols (MQTT) are still exploited in 2025–2026.
- Wireshark remains essential for validating configuration risks in real traffic.

For full portfolio context, see the main repo [README](../../README.md).
