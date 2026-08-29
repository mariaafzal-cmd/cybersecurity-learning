# Telnet

## What is Telnet?

Telnet is a network protocol that allows a user to communicate with a remote system through a command-line interface.

In a penetration testing context, an exposed Telnet service can be important to investigate because it may provide remote access to a system.

## Default Port

* TCP 23

## Telnet Enumeration

I used Nmap to check whether Telnet was running on the target:

```bash
nmap -sV -p 23 <TARGET_IP>
```

### What the command does

* `-p 23` → scans TCP port 23
* `-sV` → attempts to identify the service and version running on the port

## Connecting to Telnet

A Telnet service can be accessed using:

```bash
telnet <TARGET_IP> 23
```

If the service is available, the server may provide a login prompt or other information.

## Why is Telnet Insecure?

Telnet does not provide encryption for normal communication.

Because the communication is sent without encryption, sensitive information such as authentication data may be exposed to someone who can monitor the network traffic.

For secure remote administration, encrypted protocols such as SSH are generally preferred.

## Security Considerations

When encountering an exposed Telnet service during an authorized assessment, I would consider:

* Identifying the Telnet service and version.
* Checking whether authentication is required.
* Looking for weak or default credentials only when authorized.
* Determining whether the service is unnecessarily exposed.
* Checking whether a secure alternative such as SSH is available.

## What I Learned

* Telnet commonly runs on TCP port 23.
* Nmap can be used to identify an exposed Telnet service.
* I learned how to connect to a Telnet service from the command line.
* Telnet is insecure because its communication is not encrypted.
* Exposed remote-access services should be investigated during an authorized security assessment.

## Practice

I practiced Telnet enumeration and interaction in an authorized TryHackMe training environment as part of the **Network Services** room.

