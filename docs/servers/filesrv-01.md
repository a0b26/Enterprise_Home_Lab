# FILESRV-01 - File Server

## Purpose

FILESRV-01 provides centralised file storage and SMB network sharing for domain joined devices within the home lab.

The server is intended to demonstrate Windows Server file services, Active Directory integration, network permissions, access control and data management.

This document covers the server configuration and operational setup. For the wider Active Directory architecture:

- [Domain Configuration](../active-directory/domain.md)
- [DNS Configuration](../active-directory/dns.md)
- [Users and Groups](../active-directory/users-groups.md)

## Virtual Machine Configuration

| Setting | Configuration |
|---|---|
| VM name | `FILESRV-01` |
| VM ID | `103` |
| Operating system | Windows Server 2019 |
| vCPU | 2 |
| Memory | 2 GB |
| OS disk | 40 GB |
| Data disk | 60 GB |
| Network bridge | vmbr1 |

The virtual machine is hosted on Proxmox VE and connected to the isolated lab network through `vmbr1`.

The operating system and data disks are separated to provide distinct locations for system files and shared data.

## Network Configuration

| Setting | Configuration |
|---|---|
| Hostname | `FILESRV-01` |
| IP address | `192.168.10.30` |
| Subnet mask | `255.255.255.0` |
| Default gateway | `192.168.10.1` |
| Preferred DNS | `192.168.10.10` |
| Network | Lab network (`192.168.10.0/24`) |

The server uses OPNsense as its default gateway and the domain controller as its preferred DNS server.

Refer to the [IP Addressing Plan](../architecture/ip-addressing.md) for the complete network allocation.

## Active Directory Integration

FILESRV-01 is intended to operate as a member server within the `ad.home.arpa` Active Directory domain.

Domain integration allows access to shared resources to be managed through domain user and security groups rather than relying solely on local accounts.

| Setting | Configuration |
|---|---|
| Domain | `ad.home.arpa` |
| NetBIOS domain | `HOME` |
| Domain controller | `WINDC-01` |
| Domain membership | `Joined` |

## Storage Configuration

The server uses separate virtual disks for the operating system and shared data.

| Volume | Purpose | Size |
|---|---|---:|
| C: | Windows Server operating system | 40 GB |
| D: | Shared data and file storage | 60 GB |

The intended data volume layout is:

```text
D:\
└── Shares\
    └── Department\
