---
layout: default
title: "Reconnaissance and Enumeration Report"
date: 2026-02-23 12:00:00 -0400
categories: pentesting labs
---

# Reconnaissance and Enumeration Report
**Course:** ITC 4610 Penetration Testing  
**Prepared by:** Mandip Amgain  
**Date:** February 23, 2026  

## 1. Introduction
The purpose of this assignment is to conduct passive and active reconnaissance against a controlled virtualized sandbox environment. This phase of a penetration test is critical for identifying the attack surface, mapping the network hierarchy, and discovering specific service versions that may contain exploitable vulnerabilities.

### 1.1 Environment Overview
The lab environment consists of an isolated internal network named `Pentest_Internal_Net` using the private IP range `100.64.0.0/24`. The systems involved include:
* **Kali Linux:** The primary attacker platform.
* **Windows Server 2019:** Acting as the Domain Controller (DNS/DHCP).
* **Metasploitable2:** A Linux-based target designed with intentional vulnerabilities.
* **Windows 7:** A legacy domain-joined client system.

## 2. Passive Reconnaissance
Passive reconnaissance involves gathering information without directly interacting with the target’s systems, thereby minimizing the attacker’s digital footprint.

### 2.1 Tools and Features
* **WHOIS:** Used to query public record information and domain ownership.
* **nslookup:** A tool for IP address and device name searches.
* **theHarvester:** Used to find email addresses and infrastructure details for an organization.

### 2.2 Methodology and Findings
In this lab, `nslookup` was utilized to verify the internal DNS structure of the `pentest.lab` domain.
*(Figure 1: Successful nslookup resolution showing pentest.lab mapping to 100.64.0.10)*

**Analysis:** The tool successfully identified the Domain Controller at `100.64.0.10`. Initial attempts failed due to service connectivity issues, which were resolved by manually pointing the attacker's DNS settings to the server.

## 3. Active Reconnaissance
Active reconnaissance involves direct interaction with the target systems to identify open ports and active services.

### 3.1 Tools and Features
* **Nmap:** A command-line tool used for network discovery and service version detection.
* **Wireshark:** A graphical scanner used for real-time packet analysis and traffic monitoring.
* **Netcat:** A "banner grab" tool used to manually identify service headers.

### 3.2 Traffic Analysis
Wireshark was used to monitor communication between the Kali Linux attacker and the Windows Server.
*(Figure 2: Wireshark capture showing ICMP (Ping) traffic between 100.64.0.60 and 100.64.0.10.)*

**Analysis:** This capture verified that the network layer was fully functional despite initial DHCP failures.

## 4. Enumeration: List of Findings
Enumeration is the process of extracting detailed information about the target's services.

### 4.1 Detailed Service Mapping
*(Figure 3: Nmap version scan (-sV) results for the Metasploitable2 target 100.64.0.40)*

**Target Findings (Consolidated from Nmap, Netcat, and nslookup):**

| Target Host | OS / Role | Open Ports | Identified Service & Version | Vulnerability Notes |
| :--- | :--- | :--- | :--- | :--- |
| `100.64.0.10` | Win Server 2019 / Domain Controller | 53, 88, 389, 445 | DNS (ISC BIND), Kerberos, LDAP, SMB | Primary target for Active Directory attacks. |
| `100.64.0.40` | Metasploitable2 / Vulnerable Linux | 21, 22, 25, 80, 3306 | vsFTPd 2.3.4, OpenSSH 4.7p1, Apache 2.2.8, MySQL | Contains multiple high-risk service backdoors (vsFTPd). |
| `100.64.0.30` | Windows 7 / Legacy Client | 135, 139, 445 | RPC, NetBIOS, SMB | Legacy system susceptible to SMB exploits. |
| `100.64.0.50` | DVWA / Vulnerable Web App | 80 | Apache httpd (via PHP 5.2.4) | Prime target for web-app testing (SQLi, XSS). |

*(Figure 4: Manual banner grabbing using Netcat confirmed the vsFTPd 2.3.4 version string.)*

## 5. Network Management and Troubleshooting
A significant portion of the reconnaissance phase involved resolving environment configuration issues.
* **DHCP Failures:** Multiple systems, including Windows 7, initially defaulted to APIPA addresses (169.254.x.x).
* **Resolution:** Static IP addresses were manually assigned (e.g., 100.64.0.30 for Windows 7) to ensure they remained within the internal network range.

## 6. Conclusion
The reconnaissance phase successfully mapped the internal lab environment. By combining passive DNS queries with active Nmap scans and banner grabbing, a detailed list of vulnerable services was established for further exploitation testing.


