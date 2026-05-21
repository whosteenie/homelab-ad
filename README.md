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

Client01 - Windows 11 Enterprise (pending)  
  IP: 192.168.100.10 (planned)  

---

## Domain Controller Setup

Spun up a Windows Server 2025 VM in Hyper-V using an internal virtual switch
to keep lab traffic isolated from the host network. Installed the AD DS role
and promoted the server to a Domain Controller for a new forest at lab.local.
Set a static IP of 192.168.100.1 with DNS pointing to itself (127.0.0.1) since
it's acting as the DNS server for the domain.

---

## Active Directory Configuration

### Organizational Units

Created two OUs at the domain root to keep users and computers separate.
This makes it easier to apply Group Policy independently to each.

- IT
- Workstations

### Users

Created two user accounts in the IT OU to use for testing and policy verification.

- jsmith (John Smith)
- jdoe (Jane Doe)

### Groups

Created a Global Security Group called IT Staff in the IT OU and added both
users as members. Grouping users this way makes permission management cleaner
since you assign access to the group rather than individual accounts.

### Group Policy

Created a GPO called IT Policy and linked it to the IT OU. Configured a policy
to prevent users from changing the desktop background. This will be verified
once Client01 joins the domain and logs in as jsmith or jdoe.

---

## Client VM Setup

In progress.
