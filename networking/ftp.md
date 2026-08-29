# FTP — File Transfer Protocol

## What is FTP?

FTP (File Transfer Protocol) is a network protocol used to transfer files between a client and a server.

During penetration testing, an FTP service can be interesting to investigate because misconfigured servers may expose files or allow unauthorized access.

## Default Port

* TCP 21

## FTP Enumeration

I used Nmap to identify the FTP service and determine its version:

```bash
nmap -sV -p 21 <TARGET_IP>
```

### What the command does

* `-p 21` → scans port 21
* `-sV` → attempts to identify the service and version

## Connecting to FTP

I can connect to an FTP server using:

```bash
ftp <TARGET_IP>
```

## Useful FTP Commands

| Command | Purpose                    |
| ------- | -------------------------- |
| `ls`    | List files and directories |
| `pwd`   | Show the current directory |
| `cd`    | Change directory           |
| `get`   | Download a file            |
| `put`   | Upload a file              |
| `bye`   | Exit FTP                   |

## Anonymous Access

Some FTP servers may allow anonymous login.

Anonymous access is important during enumeration because it may allow access to files without providing normal user credentials.

## Security Considerations

* FTP does not provide encryption by default.
* Anonymous access can expose files if incorrectly configured.
* Weak credentials can create security risks.
* Sensitive files should not be unnecessarily exposed through an FTP service.

## What I Learned

* How to identify an FTP service using Nmap.
* How to connect to an FTP server.
* How to navigate an FTP server.
* How to download files using `get`.
* Why anonymous FTP access should be checked during enumeration.
* Why unencrypted FTP is considered insecure.

## Practice

I practiced these concepts in an authorized TryHackMe training environment as part of the **Network Services** room.
