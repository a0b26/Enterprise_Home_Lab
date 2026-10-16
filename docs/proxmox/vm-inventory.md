# Virtual Machine Inventory

## Purpose

This document records the virtual machines deployed in the Home Lab, their assigned resources, network connections and responsibilities.

## Current Inventory

| VM ID | Name | Operating System | Virtual CPU | RAM | OS Disk | Network |
|---:|---|---|---:|---:|---|---|
| 100 | `WINDC-01` | Windows Server 2022 | 2 | 4 GB | 60 GB | `vmbr1` |
| 101 | `WIN11-01` | Windows 11 | 2 | 4 GB | 40 GB | `vmbr1` |
| 102 | `OPNsense-01` | OPNsense | 2 | 2 GB | 16 GB | `vmbr0`, `vmbr1` |
| 103 | `FILESRV-01` | Windows Server 2019 Evaluation | 2 | 2 GB | 40 GB | `vmbr1` |

## VM Roles

### OPNsense-01

**Purpose:** Firewall and router for the isolated laboratory network.

Responsibilities:

- Routes traffic between the lab network and the home network.
- Provides the lab default gateway.
- Performs outbound NAT for lab Internet access.
- Enforces firewall rules between network segments.

Network interfaces:

- `net0` → `vmbr0` (WAN)
- `net1` → `vmbr1` (LAN)

### WINDC-01

**Purpose:** Active Directory domain controller and DNS server.

Operating system: Windows Server 2022

Responsibilities:

- Active Directory Domain Services.
- DNS for the `ad.home.arpa` domain.
- Domain authentication.
- Group Policy management.
- Centralised identity and access management for domain joined systems.

### WIN11-01

**Purpose:** Primary Windows domain workstation.

Operating system: Windows 11 Enterprise 25H2

Responsibilities:

- Tests domain authentication and domain joining.
- Validates DNS resolution and domain controller discovery.
- Provides a client for Group Policy testing.
- Tests access to SMB file shares and other domain resources.

### FILESRV-01

**Purpose:** Windows file server and server upgrade test environment.

Operating system: Windows Server 2019.

Responsibilities:

- Hosts SMB file shares.
- Uses Active Directory groups to manage resource access.
- Provides an environment for testing NTFS and share permissions.
- Supports testing of domain based authentication and Kerberos SSO.
- Provides a platform for future server migration exercises.

## Future Workloads

Potential additions include:

- Linux domain integrated client.
- Centralised logging and monitoring.
- Dedicated security testing VM.
- Additional Windows Server versions for migration exercises.
- Additional isolated networks and VLANs.

New workloads will be introduced according to available resources and their value to the lab's learning objectives.

## Maintenance

- This section will be updated whenever a VM is created, removed, renamed or fundamentally reconfigured or repurposed.
