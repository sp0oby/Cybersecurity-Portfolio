# Project 1: Security Audit & Vulnerability Identification for Small Business

This folder contains documentation, scans, and reports for **Project 1** of my cybersecurity portfolio.

As part of the **SecureTech Solutions** simulation, this project focuses on conducting a security audit of the company's backend server to identify vulnerabilities typical in small businesses, such as misconfigured web applications and exposed services.

## Project Overview

- **Objective**  
  Perform an initial security audit using Nmap for reconnaissance and OpenVAS (GVM) for vulnerability scanning on the SecureTech-Server VM (running DVWA as a vulnerable web app). Identify risks, prioritize them (e.g., using CVSS scores), and recommend mitigations.

- **Company Context**  
  SecureTech Solutions, a mid-sized tech firm, deploys a legacy internal web portal (DVWA) for data entry. This audit simulates discovering common small-business issues like SQL injection or insecure ports, which could lead to data breaches.

- **Skills Demonstrated**  
  - Network scanning  
  - Vulnerability assessment  
  - Report generation  
  - Risk prioritization

- **Tools Used**  
  - Nmap (for port/service/OS detection)  
  - OpenVAS/GVM (for automated vulnerability scanning)

- **Key Findings Summary**  
  Detected critical SQL injection (CVSS 9.8), XSS, and open ports exposing the database.

## Files in This Folder

- `nmap-scan-results.txt`  
  Raw output from Nmap scans.

- `openvas-report.pdf`  
  Exported vulnerability report from OpenVAS.

- `audit-report.md`  
  Full write-up with findings, analysis, and recommendations.

## Setup Notes

- **Target**: SecureTech-Server VM (192.168.56.101) with DVWA at  
  http://192.168.56.101/dvwa (set to Low security for testing)

- **Performed from**: Kali-Tools VM (192.168.56.103)

## Lessons Learned

- Small businesses often overlook web application vulnerabilities in internal tools—regular audits are crucial.
- Tools like OpenVAS automate detection but require manual verification to avoid false positives.

For the full portfolio context, including the overall lab setup and other projects, see the main repository [README](../README.md).

---
Last updated: January 2026
