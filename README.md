# Active Directory Home Lab

## Overview

Home lab built using Hyper-V on Windows 11 Pro to practice Active Directory,
user management, group policy, and domain administration.

## Environment

Host: Windows 11 Pro, 32GB DDR5  
Hypervisor: Hyper-V  
Domain Controller: Windows Server 2025 Standard Evaluation  
Client VMs: Windows 11 Enterprise Evaluation

## Topology

DC01 - Windows Server 2025 (Domain Controller, DNS Server)
  IP: 192.168.100.1
  Domain: lab.local

Client01 - Windows 11 Enterprise (domain joined)
  IP: 192.168.100.10

---

## Domain Controller Setup

Spun up a Windows Server 2025 VM in Hyper-V using an internal virtual switch
to keep lab traffic isolated from the host network. Installed the AD DS role
and promoted the server to a Domain Controller for a new forest at lab.local.
Set a static IP of 192.168.100.1 with DNS pointing to itself (127.0.0.1) since
it acts as the DNS server for the domain.

---

## Active Directory Configuration

### Organizational Units

Created two OUs at the domain root to keep users and computers separate,
making it easier to apply Group Policy independently to each.

- IT
- Workstations

### Users and Groups

Created two user accounts in the IT OU for testing and policy verification.

- jsmith (John Smith)
- jdoe (Jane Doe)

Both accounts were added to a Global Security Group called IT Staff.
Grouping users this way makes permission management cleaner since you
assign access to the group rather than individual accounts.

<p align="center">
  <img src="screenshots/ad-users-groups.png" alt="Users and IT Staff group in Active Directory Users and Computers"/>
</p>
<p align="center"><em>Users and IT Staff group inside the IT OU</em></p>

### Group Policy

Created a GPO called IT Policy and linked it to the IT OU. Configured a policy
to prevent users from changing the desktop background.

<p align="center">
  <img src="screenshots/gpm-ou-policy.png" alt="Group Policy Management showing IT Policy linked to IT OU"/>
</p>
<p align="center"><em>IT Policy linked to the IT OU in Group Policy Management</em></p>

---

## Client VM Setup

Spun up a Windows 11 Enterprise VM in Hyper-V on the same internal switch.
Set a static IP of 192.168.100.10 with the DC as the default gateway and DNS
server. Verified connectivity to DC01 via ping before joining the domain.

<p align="center">
  <img src="screenshots/ping.png" alt="Ping from Client01 to DC01 showing successful connectivity"/>
</p>
<p align="center"><em>Successful ping from Client01 to DC01 confirming network connectivity</em></p>

Joined Client01 to lab.local through System Properties using domain admin
credentials. After rebooting, logged in as LAB\jsmith and confirmed the
domain user profile was created and Group Policy applied correctly.

<p align="center">
  <img src="screenshots/GPO-background.png" alt="jsmith logged in as a domain user with background policy enforced"/>
</p>
<p align="center"><em>jsmith logged in as a domain user with the background policy enforced</em></p>

The background settings page shows "Some of these settings are managed
by your organization" and the options are grayed out, confirming the
GPO is applying as expected.

---

## What's Next

- Create additional GPOs (password policy, drive mapping, software restriction)
- Move Client01 computer account into the Workstations OU
- Practice user account management (disable, unlock, reset password)
- Explore PowerShell for AD administration
