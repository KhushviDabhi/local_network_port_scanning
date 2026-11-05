# Task 1: Scan Your Local Network for Open Ports

## Objective
Use Nmap to scan an authorized local-network device, identify TCP ports and understand their states and services.

## Tools
- Windows Command Prompt
- Nmap 7.993
- Zenmap

## Network details
- Computer IPv4 address: `192.168.1.81`
- Subnet mask: `255.255.255.0`
- Default gateway / scanned router: `192.168.1.1`
- Local network range identified: `192.168.1.0/24`

## Commands
The subnet scan was run in Zenmap using `192.168.1.0/24`. The saved original report is for the router at `192.168.1.1`.

```cmd
ipconfig
nmap -sT 192.168.1.0/24
nmap -sT -oN "%USERPROFILE%\Desktop\Task1_Scan_Report.txt" 192.168.1.1
```

`-sT` performs a TCP connect scan. `-oN` saves Nmap's normal text output.

## Actual saved scan findings
The router `192.168.1.1` was up. Three TCP ports were reported open:
- `53/tcp` — DNS (`domain`)
- `80/tcp` — HTTP (`http`)
- `443/tcp` — HTTPS (`https`)

These ports were reported filtered:
- `21/tcp` — FTP
- `22/tcp` — SSH
- `23/tcp` — Telnet
- `139/tcp` — NetBIOS session service
- `161/tcp` — SNMP
- `445/tcp` — Microsoft-DS / SMB
- `3517/tcp` — 802.11 IAPP
- `8082/tcp` — Nmap service label `blackice-alerts`

Nmap reported 989 other scanned TCP ports as closed. A filtered result means Nmap could not determine whether the port was open or closed, often because packet filtering prevented a conclusive response.

## Security observations
- DNS (53): commonly needed by routers. Risk depends on DNS configuration and exposure.
- HTTP (80): unencrypted. Sensitive information should not be entered over an untrusted HTTP connection.
- HTTPS (443): encrypted, but security still depends on firmware, TLS configuration and authentication.
- Filtered ports are not confirmed vulnerabilities. Keep router firmware updated, disable unneeded services, use strong administrator credentials and restrict administration to trusted devices.

An open port alone does not prove a vulnerability. No exploitation was performed.

## Files
- `README.md` — this explanation.
- `Task1_Scan_Report.txt` — original Nmap output supplied.
- `commands.txt` — commands used.
- `scan_findings.csv` — structured port results.
- `screenshots` — available practical screenshots.

## Conclusion
The TCP connect scan confirmed that the router at `192.168.1.1` was reachable and found three open TCP ports (53, 80 and 443), plus several filtered ports. The original Nmap output is included as the primary scan evidence.
