# Enterprise_Home_Lab
A virtualised enterprise style IT infrastructure lab built with Proxmox VE, OPNsense and Windows/Linux systems based upon the foundation of the Australian Signals Directorate Essential Eight principles.

## Objectives

This lab is designed to develop practical skills in:

- Virtualisation and Infrastructure Administration
- Networking and Firewalling
- Active Directory and DNS
- Group Policy
- Windows and Linux Administration
- Identity and Access Management
- Endpoint Security
- Backup and Recovery
- Infrastructure Troubleshooting
- Security Governance and Risk Management
- Data Privacy
- Logging and Audit Trails
- Incident Response
- Vulnerability Management
- Change Management

## Current Architecture

- Proxmox VE - Hypervisor
- Isolated laboratory network (OPNsense Firewall/Router)
- Windows Server 2022 Domain Controller
- Windows 11 Domain Workstation
- Windows Server 2019 File Server

## Network

Home network:
`192.168.50.0/24`

Lab network:
`192.168.10.0/24`

The laboratory network is isolated from the home LAN through OPNsense.

## Active Directory

Domain:
`ad.home.arpa`

NetBIOS:
HOME

Domain Controller:
WINDC-01

## Status

- [x] Proxmox installed
- [x] VM storage configured
- [x] OPNsense deployed
- [x] Isolated lab network created
- [x] Windows Server 2022 DC deployed
- [x] Active Directory configured
- [x] DNS configured
- [x] Windows 11 domain client deployed
- [x] Group Policy configured
- [x] Windows Server 2019 file server deployed
- [ ] SMB permissions
- [ ] GPO application deployment
- [ ] Linux domain integration
- [ ] VLAN segmentation
- [ ] Security testing environment
- [ ] Server migration exercises
