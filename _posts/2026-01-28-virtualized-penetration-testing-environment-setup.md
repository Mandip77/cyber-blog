---
layout: default
title: "Virtualized Penetration Testing Environment Setup"
date: 2026-01-28 12:00:00 -0400
categories: pentesting labs setup
---

# Virtualized Penetration Testing Environment Setup
**Course Title:** ITC 4610 Penetration Testing  
**Professor:** Betty J. Lauer  
**Prepared by:** Mandip Amgain  
**Date:** January 28, 2026  

## Introduction
This project involved designing and implementing a virtualized penetration testing environment to safely practice security assessment techniques. The lab simulates an enterprise network using multiple operating systems connected through an isolated internal network.

## Virtualization Platform
Oracle VirtualBox was selected as the hypervisor because it is free, stable, and beginner friendly. It supports both ISO-based installations and preconfigured virtual machines, making it ideal for building a penetration testing lab.

## Network Configuration
All virtual machines were connected to a VirtualBox internal network named `Pentest_Internal_Net` using the private IP range `100.64.0.0/24`. The internal network prevents internet exposure while allowing full communication between lab systems.

*(Figure 1. Kali Linux VirtualBox network adapter configuration showing Adapter 1 attached to the internal network Pentest_Internal_Net)*

*(Figure 2. Illustrates the internal network architecture of the penetration testing lab, including IP addressing, operating system roles, and system connectivity)*

## Virtual Machines and Roles
1. **Windows Server 2019** was configured as a domain controller providing Active Directory, DNS, and DHCP services for the network.
2. **Windows 7** functioned as a domain-joined client system, representing a legacy endpoint.
3. **Kali Linux and Parrot Linux** were used as attacker machines for penetration testing activities.
4. **Metasploitable2 and DVWA** served as intentionally vulnerable targets for exploitation and web-application testing.

*(Figure 3. Oracle VirtualBox Manager displaying the configured virtual machines used in the penetration testing lab environment)*

## Testing and Validation
Basic functionality was verified by confirming system boot, IP address assignment via DHCP, and network connectivity. Kali Linux successfully communicated with all targets, confirming correct configuration.

## Conclusion
This virtual lab provides a controlled environment for learning penetration testing techniques while maintaining safety and isolation. The design mirrors real-world enterprise networks and supports future security testing exercises.


