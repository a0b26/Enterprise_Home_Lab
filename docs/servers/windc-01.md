# WINDC-01 - Domain Controller

## Purpose

WINDC-01 provides the central identity and name resolution services for the home lab through Active Directory Domain Services and DNS.

It is responsible for domain authentication, directory management and internal name resolution for domain joined lab systems.

Detailed Active Directory Configuration:

- [Domain Configuration](../active-directory/domain.md)
- [DNS Configuration](../active-directory/dns.md)
- [OU Structure](../active-directory/ou-structure.md)
- [Users and Groups](../active-directory/users-groups.md)
- [Group Policy](../active-directory/group-policy.md)

## Virtual Machine Configuration

| Setting | Configuration |
|---|---|
| VM name | `WINDC-01` |
| VM ID | `100` |
| Operating system | Windows Server 2022 |
| vCPU | 2 |
| Memory | 4 GB |
| Virtual disk | 60 GB |
| Storage | Proxmox local-lvm (SSD) |
| Network bridge | vmbr1 |

## Network Configuration

| Setting | Configuration |
|---|---|
| Hostname | `WINDC-01` |
| IP address | `192.168.10.10` |
| Subnet mask | `255.255.255.0` |
| Default gateway | `192.168.10.1` |
| Preferred DNS | `192.168.10.10` |
| Network | Lab network (`192.168.10.0/24`) |

The domain controller uses a static IP address to provide a consistent endpoint for domain joined clients.

The server uses OPNsense as its default gateway, whilst DNS queries are handled locally through its DNS service.

Refer to the [IP Addressing Plan](../architecture/ip-addressing.md) for the complete network allocation.

## Installed Roles and Services

| Role / Service | Purpose | Status |
|---|---|---|
| Active Directory Domain Services | Centralised directory and domain authentication | Implemented |
| DNS Server | Internal name resolution and domain service records | Implemented |
| DHCP Server | Centralised address allocation | Future consideration |

## Active Directory Configuration

| Setting | Configuration |
|---|---|
| Domain name | `ad.home.arpa` |
| NetBIOS name | `HOME` |
| Domain controller | `WINDC-01` |
| Domain functional level | Windows Server 2016 |
| Forest functional level | Windows Server 2016 |

Current configuration includes:

- An organisational unit structure for administrative accounts, users, workstations, servers and groups.
- Dedicated administrative and standard user accounts.
- Security groups for managing access.
- Group Policy Objects for workstation configuration and security baselines.

See the individual Active Directory documents for further details.

## Security and Administration

The domain controller is a critical infrastructure component and needs particular attention when managing privileged access.

Security considerations include:

- Restricting administrative access to authorised accounts.
- Separating ordinary user accounts from privileged accounts.
- Applying appropriate domain controller security policies.
- Maintaining reliable DNS configuration.
- Monitoring authentication and directory-related events.
- Maintaining regular VM backups.

The `lab.admin` account has been configured for administrative duties within the lab. Ordinary workstation activities use a standard user account.

## Validation and Testing

| Test | Expected result | Status |
|---|---|---|
| Domain services | AD DS services are operational | Implemented Successfully |
| DNS resolution | Internal domain names resolve correctly | Implemented Successfully |
| External DNS forwarding | External names resolve through OPNsense | Tested Successfully |
| Domain authentication | Domain users can authenticate successfully | Tested Successfully |
| Group Policy | Relevant GPOs are applied to appropriate devices | Tested Successfully |
| Backup and recovery | Domain services can be restored from backup | Pending verification |

## Future Improvements

Possible improvements include:

- Introducing a second domain controller.
- Implementing DHCP and DHCP scopes.
- Configuring DHCP relay through OPNsense if DHCP is centralised on Windows.
- Introducing centralised security event collection.
- Reviewing privileged access and administrative delegation.
- Implementing additional domain controller security baselines.
- Testing domain controller backup and recovery procedures.
