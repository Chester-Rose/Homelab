# Infrastructure Build

## Objective
Build a domain environment to practice Windows Server administration and support tasks.

## Topology
![Topology](../diagrams/homelab-topology.png)

| VM | Role | IP | Notes |
|----|------|----|-------|
| DC01 | Domain Controller, DNS, DHCP | 172.16.0.1 | Static |
| CLIENT01 | Domain-joined client | 172.16.0.100 | DHCP |

## Build Steps (high level)
1. Created internal network in VirtualBox named `intnet`.
2. Installed Windows Server 2019, renamed to DC01, set static IP 172.16.0.1.
3. Installed AD DS role, promoted to Domain Controller for `homelab.local`.
4. Installed and configured DNS (forward and reverse zones).
5. Installed and configured DHCP with scope 172.16.0.100–172.16.0.200.
6. Created Windows 10 VM, attached to `intnet`, joined to domain.

## Screenshots
- [`screenshots/dns-manager.png`](screenshots/dns-manager.png) — forward lookup zone
- [`screenshots/dhcp-scope.png`](screenshots/dhcp-scope.png) — DHCP scope and lease
- [`screenshots/domain-join.png`](screenshots/domain-join.png) — successful join
- [`screenshots/ipconfig-client.png`](screenshots/ipconfig-client.png) — client DNS pointing to DC

## Troubleshooting
See [troubleshooting.md](troubleshooting.md) for issues encountered and fixes.