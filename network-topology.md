# Network Topology

## Design

The physical home LAN uses `192.168.50.0/24`.

The homelab is placed on a separate virtual network using
`192.168.10.0/24`.

OPNsense provides routing and firewalling between the two
networks.

## Networks

| Network | CIDR | Purpose |
|---|---|---|
| Home | 192.168.50.0/24 | Physical network |
| Lab | 192.168.10.0/24 | Isolated virtual lab |

## Devices

| Host | IP | Purpose | Operating System |
|---|---|---|---|
| Proxmox | 192.168.50.200 | Hypervisor | 
| OPNsense LAN | 192.168.10.1 | Lab gateway |
| WINDC-01 | 192.168.10.10 | AD/DNS | Windows Server 2022 |
| WIN11-01 | 192.168.10.20 | Domain workstation | Windows 11 Enterprise |
| FILESRV-01 | 192.168.10.30 | File server | Windows Server 2019 |
