# Homelab

A virtualized Windows environment built to practice Active Directory, DNS, DHCP, Group Policy, and infrastructure monitoring.

## Environment
- **Hypervisor:** Oracle VirtualBox
- **Server:** Windows Server 2025 (DC01)
- **Client:** Windows 11 Pro (CLIENT01)
- **Domain:** homelab.local
- **Internal network:** 172.16.0.0/24

## What's in this repo
- [`infrastructure/`](infrastructure/) — how the lab was built (AD DS, DNS, DHCP, domain join)
- [`labs/`](labs/) — hands-on exercises run inside the environment

## Labs completed
- [GPO Software Deployment](labs/01-gpo-software-deployment/)
- [Account Lockout Policy & Troubleshooting](labs/02-account-lockout-policy/)
- [PRTG Infrastructure Monitoring](labs/03-prtg-monitoring/)

## Skills demonstrated
Windows Server, Active Directory, DNS, DHCP, Group Policy, VirtualBox, troubleshooting, documentation.