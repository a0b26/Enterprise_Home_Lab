# Design Decisions

This document provides a list of Architecture Decision Records made as this project has evolved.

## ADR-001 - Initial Operating System Choices

### Domain Controller

**Decision:** Use Windows Server 2022 for the Domain Controller

**Reason:** 2022 was chosen for this project due to its proven reliability and the option to practice an in-place upgrade to Windows Server 2025 later on.

**Alternative Considered:** Use Windows Server 2025 as it is the latest version.

**Rejected Because:** WS2025 can be saved for an upgrade later on.

### Client Workstations

**Decision:** Use Windows 11 25H2.

**Reason:** Windows 11 Enterprise 25H2 was chosen for client workstations to connect to the domain as this was the latest release in August 2026.

**Alternative Considered:** Linux 

**Rejected Because:** Lab is structured like a typical business environment, where Windows is most often used. Linux workstations are planned to be added later on.

### Firewall/Routing

**Decision:** Use OPNsense

**Reason:** OPNsense was chosen as it provides a full featured, open source firewall and routing platform built on FreeBSD which is optimised for virtualised environments.

**Alternative Considered:** PFsense

**Rejected Because:** Chose OPNsense instead of pfSense as it is fully open source with paywalls.
<br><br>

## ADR-002 - Isolating the laboratory network

**Decision:** Use a separate 192.168.10.0/24 virtual network behind OPNsense.

**Reason:** The lab contains intentionally experimental systems and security configurations. Directly placing these systems on the home LAN increases the potential impact of misconfiguration or compromise.

**Security consideration:** Traffic between the lab and home network is controlled through firewall policy.

**Alternative considered:** Place all VMs directly on 192.168.50.0/24.

**Rejected Because:** This would provide insufficient network isolation for security experimentation.
<br><br>

## ADR-003 - Separate DC and File Server

**Decision:** Run the File Server from a separate Windows Server 2019 VM.

**Reason:** Separating roles ensures a Domain Controller only functions as a identity provider without resource contention from heavy file transfers.

**Security Consideration:** Isolating the file server restricts the ransomware blast radius and prevents granting attackers immediate automated Domain Admin privileges over the entire network.

**Alternative Considered:** Consolidating the DC and File Server into a single VM.

**Rejected Because:** Combining the roles creates a single point of failure.
<br><br>

## ADR-004 - Static addressing for infrastructure

**Decision:** Use static IP addresses for core infrastructure systems within the laboratory network.

**Reason:** Core infrastructure services such as the firewall, Domain Controller/DNS server and file server need predictable network addresses.

Static addressing simplifies:

- DNS configuration
- Active Directory service discovery
- Firewall rules
- Troubleshooting
- Administration and documentation

**Security / Operational Considerations:** Predictable addressing makes infrastructure easier to identify and manage.
unexpectedly.

- Static addressing is limited to infrastructure systems. End user workstations and future general purpose clients will use DHCP.

**Alternative Considered:** Use DHCP for all laboratory systems.

**Rejected Because:** Dynamic addresses for core infrastructure would introduce unnecessary dependency on DHCP and could complicate DNS, firewall rules and service discovery.
<br><br>

## ADR-005 - Backups to separate physical storage

**Decision:** Store Proxmox VM backups on a physically separate HDD rather than relying exclusively on the primary SSD used by the Proxmox host and active VM storage.

**Reason:** Separating backup storage from primary VM storage reduces the risk that a failure of the primary SSD will result in loss of the backups.

The additional storage also provides capacity for:

- Full VM backups
- Backup retention
- Larger VM workloads
- File server data
- Future lab expansion

**Security / Operational Considerations:** Backups should be tested periodically to ensure they can be restored. The lab currently contains no production data so the backup strategy is intended to allow recovery from configuration mistakes, VM corruption and hardware failure.

**Alternative Considered:** Store backups on the main SSD.

**Rejected Because:** SSD failure would affect both the VMs and the backups.
