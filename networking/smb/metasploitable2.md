# SMB Exploitation — Metasploitable 2

## Lab Environment

- Attacker: Kali Linux
- Target: Metasploitable 2
- Network: Local virtual lab

## Objective

The objective of this lab was to enumerate the SMB service,
identify misconfigurations, obtain access to an accessible SMB
share, and investigate privilege escalation opportunities.

## Attack Methodology

Nmap
↓
SMB Enumeration
↓
Anonymous Access
↓
Share Enumeration
↓
smbclient
↓
Initial Access
↓
Privilege Escalation
↓
Root
