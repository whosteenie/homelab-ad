# Active Directory Home Lab

## Overview
Home lab built using Hyper-V on Windows 11 Pro to practice Active Directory, 
user management, group policy, and domain administration.

## Environment
- Host: Windows 11 Pro, 32GB DDR5
- Hypervisor: Hyper-V
- DC01: Windows Server 2025 Standard Evaluation
- Client VMs: Windows 11 Enterprise Evaluation

## Setup
### Phase 1 - Domain Controller
- Created internal virtual switch (LabSwitch)
- Installed Windows Server 2025 with Desktop Experience
- Installed AD DS role
- Promoted to Domain Controller
- Domain: lab.local
- Forest/Domain Functional Level: Windows Server 2025

## In Progress
- Setting static IP on DC01
- Creating client VMs
