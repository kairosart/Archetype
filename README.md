
# Archetype – Hack The Box (Starting Point)

## Overview

**Archetype** is a Windows-based Starting Point machine on Hack The Box focused on basic enumeration, SMB access, MSSQL exploitation, and Windows privilege escalation. It is designed to introduce common enterprise misconfigurations and attack paths.

- **Platform:** Windows
    
- **Difficulty:** Easy / Starting Point
    
- **Key Topics:** SMB, MSSQL, Credentials reuse, PowerShell, Privilege Escalation
    

---

## Objectives

- Enumerate exposed services
    
- Extract credentials from SMB shares
    
- Authenticate to MSSQL using leaked credentials
    
- Gain initial shell
    
- Escalate privileges to Administrator
    

---

## Enumeration

### Nmap Scan

A full TCP scan reveals the following key services:

- **SMB (445)** – File sharing enabled
    
- **MSSQL (1433)** – Microsoft SQL Server
    

These services indicate a potential enterprise environment with misconfigured access controls.

---

## SMB Enumeration

Anonymous access to SMB is enabled.

### Steps:

- List available SMB shares
    
- Access the `backups` share
    
- Download configuration files
    

### Findings:

A configuration file is found containing **plaintext credentials** for a SQL service account.

---

## MSSQL Exploitation

Using the recovered credentials:

- Authenticate to MSSQL
    
- Enable `xp_cmdshell`
    
- Execute system commands
    

This allows command execution on the target system under the SQL Server service context.

---

## Initial Foothold

A reverse shell is obtained using PowerShell via `xp_cmdshell`.

- Listener set on the attacker machine
    
- PowerShell payload executed through MSSQL
    
- Shell received as a low-privileged user
    

---

## Privilege Escalation

### Enumeration

Local enumeration reveals:

- PowerShell history file containing **Administrator credentials**
    

### Exploitation

- Switch user to Administrator using recovered credentials
    
- Gain full administrative access
    

---

## Flags

- **User Flag:** Retrieved after initial shell access
    
- **Root Flag:** Retrieved after privilege escalation
    

---

## Tools Used

- `nmap`
    
- `smbclient`
    
- `impacket-mssqlclient`
    
- `PowerShell`
    
- `netcat`
    

---

## Key Takeaways

- Never allow anonymous SMB access
    
- Avoid storing credentials in plaintext files
    
- Secure MSSQL instances and disable dangerous features like `xp_cmdshell`
    
- Clear PowerShell history files in sensitive environments
    

---

## Disclaimer

This write-up is for educational purposes only and should only be used on systems you own or have explicit permission to test.

---

Happy Hacking 🚀
