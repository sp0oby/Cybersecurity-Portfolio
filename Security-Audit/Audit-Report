# Security Audit Report  
**SecureTech Solutions Backend Server**  
**Project 1 – Security Audit & Vulnerability Identification for Small Business**

**Prepared by:** spoobs
**Date:** January 15, 2026  
**Version:** 1.0  

## Executive Summary

This audit report presents the results of an automated security scan of the SecureTech Solutions backend server (192.168.56.101). The scan used Nmap for reconnaissance and OpenVAS/GVM for vulnerability detection. One low-severity vulnerability was identified (TCP timestamps information disclosure, CVSS 2.6). No high or critical issues were found in this network-level assessment.

**Scan Date**: January 15, 2026  
**Duration**: 20:29:29 – 20:43:38 UTC  
**Overall Risk Level**: Low  
**Key Recommendation**: Disable TCP timestamps to reduce information leakage.

See `audit-scope-and-goals.md` for the original audit scope and objectives.

## Methodology

1. Reconnaissance: Nmap service/version/OS scan from Kali-Tools VM  
   Command: `nmap -sV -O 192.168.56.101 -oN nmap-scan-results.txt`
2. Vulnerability Scanning: OpenVAS/GVM task "SecureTech Audit"  
   Configuration: Full and fast  
   Target: 192.168.56.101 (SecureTech-Server with DVWA)

## Findings

### Nmap Results
- Host up with low latency
- Open port: 80/tcp – Apache httpd 2.4.58 (Ubuntu)
- OS fingerprint: Linux kernel 4.15–5.19 (97% confidence)
- 999 ports filtered (firewall present)

### OpenVAS/GVM Results
- 1 low-severity finding (filtered for QoD ≥ 70%)

| Vulnerability                          | Severity (CVSS) | Affected Component | Description                                                                 | Impact                                      | Solution                                                                 |
|----------------------------------------|-----------------|---------------------|-----------------------------------------------------------------------------|---------------------------------------------|--------------------------------------------------------------------------|
| TCP Timestamps Information Disclosure  | Low (2.6)       | general/tcp         | Host implements RFC1323/7323 timestamps, allowing remote uptime estimation | Reconnaissance aid for attackers            | Disable: `net.ipv4.tcp_timestamps = 0` in /etc/sysctl.conf; `sysctl -p` |

Full raw report: [openvas-report.pdf](openvas-report.pdf)

## Recommendations

1. **Immediate**:
   - Disable TCP timestamps on the server to eliminate uptime disclosure.
2. **Follow-up**:
   - Re-scan after mitigation to confirm resolution.
   - Perform targeted web application scanning (e.g., Nikto, OWASP ZAP) on DVWA to identify SQL injection, XSS, etc.
   - Harden Apache: Set `ServerTokens Prod` and `ServerSignature Off`.
3. **Ongoing**:
   - Schedule regular automated scans.
   - Update all packages monthly (`sudo apt update && sudo apt upgrade -y`).

## Conclusion

The audit confirms a low immediate technical risk on the backend server, with only minor information disclosure identified. This baseline assessment supports ongoing security improvements in the SecureTech Solutions lab environment.

For questions or discussion, contact me.

**Appendices**:
- Nmap raw output: `nmap-scan-results.txt`
- OpenVAS full report: `openvas-report.pdf`
