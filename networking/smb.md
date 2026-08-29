# SMB — Server Message Block

## What is SMB?

SMB (Server Message Block) is a network protocol used for sharing resources such as files and directories between systems over a network.

In penetration testing, an exposed or misconfigured SMB service can provide useful information about a target, such as available shares and other system details.

## Common Ports

SMB is commonly associated with:

* TCP 445
* TCP 139

## SMB Enumeration

I used Nmap to identify SMB services running on the target:

```bash
nmap -p 139,445 -sV <TARGET_IP>
```

### What the command does

* `-p 139,445` → scans ports 139 and 445
* `-sV` → attempts to identify the service and version

## Enumerating SMB with enum4linux

`enum4linux` can be used to gather information from Windows/Samba systems.

Example:

```bash
enum4linux <TARGET_IP>
```

Depending on the server configuration, it can provide information such as:

* Workgroup/domain information
* Users
* Shares
* Server information

## Enumerating SMB Shares

I used `smbclient` to list available SMB shares:

```bash
smbclient -L //<TARGET_IP>/
```

The `-L` option is used to list available shares.

## Connecting to an SMB Share

If a share is accessible, `smbclient` can be used to connect to it:

```bash
smbclient //<TARGET_IP>/<SHARE_NAME>
```

## Useful smbclient Commands

Once connected to an SMB share:

| Command      | Purpose                    |
| ------------ | -------------------------- |
| `ls`         | List files and directories |
| `cd`         | Change directory           |
| `pwd`        | Show current directory     |
| `get <file>` | Download a file            |
| `put <file>` | Upload a file              |
| `exit`       | Exit smbclient             |

## Anonymous Access

Some SMB servers may allow access without providing normal user credentials.

During an authorized assessment, checking whether shares permit anonymous access can help identify misconfigurations.

For example:

```bash
smbclient //<TARGET_IP>/<SHARE_NAME> -N
```

The `-N` option tells `smbclient` not to prompt for a password.

## What I Observed in the Lab

During the TryHackMe Network Services lab, I used Nmap to identify SMB and then used enumeration tools to investigate the service.

I used `enum4linux` to gather information and `smbclient` to investigate available shares.

I learned that SMB share enumeration can reveal useful information about how a server is configured.

## My Practical Workflow

During the TryHackMe Network Services room, I followed this general workflow when investigating the SMB service.

### 1. Identify SMB

First, I used Nmap to check whether SMB-related ports were open.

```bash
nmap -p 139,445 -sV <TARGET_IP>
```

### 2. Enumerate the SMB Service

After identifying SMB, I used `enum4linux` to gather additional information about the SMB server.

```bash
enum4linux <TARGET_IP>
```

### 3. Enumerate SMB Shares

I then used `smbclient` to check the available SMB shares.

```bash
smbclient -L //<TARGET_IP>/
```

### 4. Connect to an Accessible Share

After identifying an accessible share, I used `smbclient` to connect to it.

```bash
smbclient //<TARGET_IP>/<SHARE_NAME>
```

### 5. Investigate the Share

Once connected, I used commands such as:

```text
ls
pwd
cd
get
```

to navigate and investigate the contents of the share.

### Workflow Summary

```text
Nmap
  ↓
Identify SMB
  ↓
enum4linux
  ↓
Enumerate SMB Shares
  ↓
smbclient
  ↓
Connect to Accessible Share
  ↓
Investigate Share Contents
```

## Security Considerations

* SMB services should not be unnecessarily exposed to untrusted networks.
* Misconfigured shares may expose sensitive files.
* Anonymous access should be disabled when it is not required.
* Weak authentication can increase the risk of unauthorized access.
* SMB implementations should be kept updated and securely configured.

## What I Learned

* SMB is commonly associated with TCP ports 445 and 139.
* Nmap can be used to identify SMB services.
* `enum4linux` can help gather information about SMB/Samba systems.
* `smbclient` can be used to enumerate and interact with SMB shares.
* Share permissions are important when assessing SMB security.
* Anonymous access should be checked during authorized enumeration.

## Practice

I practiced these SMB enumeration techniques in an authorized TryHackMe training environment as part of the **Network Services** room.



