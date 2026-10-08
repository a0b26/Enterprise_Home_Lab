# IP Addressing

This document defines the IP addressing scheme used by the network.

## Static Infrastructure

| Host | IP Address | Function |
|---|---|---|
| Proxmox | 192.168.50.200 | Hypervisor / Management |
| OPNsense LAN | 192.168.10.1 | Lab gateway / Firewall |
| WINDC-01 | 192.168.10.10 | Active Directory / DNS |
| WIN11-01 | 192.168.10.20 | Windows Domain Workstation |
| FILESRV-01 | 192.168.10.30 | File Server |

## Address Allocation

Static infrastructure is allocated from the lower portion of the
lab subnet to make server addresses predictable. 

WIN11-01 has also been placed in this range temporarily and will be moved once DHCP is set up.

### Reserved ranges

| Range | Purpose |
|---|---|
| 192.168.10.1–49 | Network and server infrastructure |
| 192.168.10.50–99 | Reserved for future infrastructure |
| 192.168.10.100–199 | Future DHCP client pool |
| 192.168.10.200–254 | Future/reserved |

## DNS

The Active Directory domain is: `ad.home.arpa`.

Lab clients use: `192.168.10.10` as their primary DNS server which is provided by WINDC-01.

## Gateway

OPNsense provides the default gateway for the lab:

`192.168.10.1`

Traffic from the lab to the Internet is routed through OPNsense and translated by NAT to the home network.

## DHCP

DHCP is not currently deployed on the lab network.

Currently, systems use static IP addresses but this will be added soon. The DHCP scope will be documented here once DHCP is introduced.
