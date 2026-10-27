# Infrastructure Build

## Objective



Build a domain environment to practice Windows Server administration and support tasks.

## 

## 

## Topology

!\[Topology](../diagrams/homelab-topology.png)

|VM|Role|IP|Notes|
|-|-|-|-|
|DC01|Domain Controller, DNS, DHCP|172.16.0.1|Static|
|CLIENT01|Domain-joined client|172.16.0.100|DHCP|

## 

## Build Steps (high level)

1. Created internal network in VirtualBox named `intnet`.
2. Installed Windows Server 2019, renamed to DC01, set static IP 172.16.0.1.
3. Installed AD DS role, promoted to Domain Controller for `homelab.local`.
4. Installed and configured DNS (forward and reverse zones).
5. Installed and configured DHCP with scope 172.16.0.100–172.16.0.200.
6. Created Windows 10 VM, attached to `intnet`, joined to domain.

## 

## Troubleshooting

See [troubleshooting.md](troubleshooting.md) for issues encountered and fixes.

## 

## Validation \& Screenshots

### 

### \### 1. The Complete Environment

### 

### <table>

### &#x20; <tr>

### &#x20;   <td width="100%" align="center">

### &#x20;     <a href="screenshots/server-and-client.png" target="\_blank">

### &#x20;       <img src="screenshots/server-and-client.png" width="100%" alt="Server and Client Side-by-Side">

### &#x20;     </a>

### &#x20;   </td>

### &#x20; </tr>

### &#x20; <tr>

### &#x20;   <td width="100%">

### &#x20;     <b>End-to-End Validation</b><br>

### &#x20;     The Domain Controller (left) shows all core roles healthy (AD DS, DHCP, DNS). The Client (right) successfully received a DHCP lease (<code>172.16.0.100</code>) and is using the DC as its DNS server (<code>172.16.0.1</code>).

### &#x20;   </td>

### &#x20; </tr>

### </table>

### 

### <br>

### 

### \### 2. Domain Controller \& Virtualization Configuration

### 

### <table>

### &#x20; <tr>

### &#x20;   <td width="50%" align="center" valign="top">

### &#x20;     <a href="screenshots/dc-ipconfig.png" target="\_blank">

### &#x20;       <img src="screenshots/dc-ipconfig.png" width="100%" alt="DC IP Configuration">

### &#x20;     </a>

### &#x20;   </td>

### &#x20;   <td width="50%" align="center" valign="top">

### &#x20;     <a href="screenshots/client-details.png" target="\_blank">

### &#x20;       <img src="screenshots/client-details.png" width="100%" alt="VirtualBox Client Settings">

### &#x20;     </a>

### &#x20;   </td>

### &#x20; </tr>

### &#x20; <tr>

### &#x20;   <td width="50%" valign="top">

### &#x20;     <b>Static IP \&amp; DNS Loopback</b><br>

### &#x20;     The DC is configured with a static IP (<code>172.16.0.1</code>). Its DNS points to loopback (<code>127.0.0.1</code>), and it has dual adapters (Internal + NAT).

### &#x20;   </td>

### &#x20;   <td width="50%" valign="top">

### &#x20;     <b>Virtualization Layer</b><br>

### &#x20;     The Windows 11 Client VM is configured to connect to the isolated <code>intnet</code> Internal Network, forcing it to rely on the DC for network services.

### &#x20;   </td>

### &#x20; </tr>

### </table>

### 

### <br>

### 

### \### 3. Active Directory Structure \& Security

### 

### <table>

### &#x20; <tr>

### &#x20;   <td width="33%" align="center" valign="top">

### &#x20;     <a href="screenshots/aduc-ou-structure.png" target="\_blank">

### &#x20;       <img src="screenshots/aduc-ou-structure.png" width="100%" alt="ADUC OU Structure">

### &#x20;     </a>

### &#x20;   </td>

### &#x20;   <td width="33%" align="center" valign="top">

### &#x20;     <a href="screenshots/aduc-admin-properties.png" target="\_blank">

### &#x20;       <img src="screenshots/aduc-admin-properties.png" width="100%" alt="Admin User Properties">

### &#x20;     </a>

### &#x20;   </td>

### &#x20;   <td width="33%" align="center" valign="top">

### &#x20;     <a href="screenshots/aduc-bulk-users.png" target="\_blank">

### &#x20;       <img src="screenshots/aduc-bulk-users.png" width="100%" alt="Bulk Users">

### &#x20;     </a>

### &#x20;   </td>

### &#x20; </tr>

### &#x20; <tr>

### &#x20;   <td width="33%" valign="top">

### &#x20;     <b>OU Structure</b><br>

### &#x20;     Custom Organizational Units (<code>\_ADMINS</code>, <code>\_USERS</code>) created to separate administrative accounts from standard users.

### &#x20;   </td>

### &#x20;   <td width="33%" valign="top">

### &#x20;     <b>Privilege Assignment</b><br>

### &#x20;     Verified that the dedicated admin account (Chester Rose) has the appropriate Domain Admin group memberships.

### &#x20;   </td>

### &#x20;   <td width="33%" valign="top">

### &#x20;     <b>Bulk User Creation</b><br>

### &#x20;     Utilized PowerShell to automate the creation of dummy users into the <code>\_USERS</code> OU for testing scale.

### &#x20;   </td>

### &#x20; </tr>

### </table>

### 

### <br>

### 

### \### 4. DHCP Services

### 

### <table>

### &#x20; <tr>

### &#x20;   <td width="50%" align="center" valign="top">

### &#x20;     <a href="screenshots/dhcp-scope.png" target="\_blank">

### &#x20;       <img src="screenshots/dhcp-scope.png" width="100%" alt="DHCP Scope">

### &#x20;     </a>

### &#x20;   </td>

### &#x20;   <td width="50%" align="center" valign="top">

### &#x20;     <a href="screenshots/dhcp-lease.png" target="\_blank">

### &#x20;       <img src="screenshots/dhcp-lease.png" width="100%" alt="DHCP Lease">

### &#x20;     </a>

### &#x20;   </td>

### &#x20; </tr>

### &#x20; <tr>

### &#x20;   <td width="50%" valign="top">

### &#x20;     <b>Active DHCP Scope</b><br>

### &#x20;     Configured the address pool (<code>172.16.0.100-200</code>) and activated the scope on the server.

### &#x20;   </td>

### &#x20;   <td width="50%" valign="top">

### &#x20;     <b>Active Address Lease</b><br>

### &#x20;     Verified that <code>CLIENT01</code> successfully negotiated a lease from the DHCP server.

### &#x20;   </td>

### &#x20; </tr>

### </table>

