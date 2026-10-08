# Lab Overview

## Purpose

This document describes the physical and virtual infrastructure currently supporting the Home Lab.

## Physical Host

| Component | Specification |
|---|---|
| CPU | Intel Core i7-860 |
| CPU cores/threads | 4 / 8 |
| RAM | 12 GB DDR3 |
| System storage | 250 GB SSD |
| Secondary storage | 750 GB HDD |
| Hypervisor | Proxmox VE |

## Virtual Infrastructure

| VM | OS | vCPU | RAM | Storage | Network | Purpose |
|---|---|---:|---:|---:|---|---|
| OPNsense-01 | OPNsense | 2 | 3 GB | 16 GB | vmbr0/vmbr1 | Firewall/router |
| WINDC-01 | Windows Server 2022 | 2 | 4 GB | 60 GB | vmbr1 | AD DS / DNS |
| WIN11-01 | Windows 11 | 2 | 4 GB | 40 GB | vmbr1 | Domain workstation |
| FILESRV-01 | Windows Server 2019 | 2 | 2 GB | 40 GB + 60 GB | vmbr1 | File server |

## Storage

### SSD

Used for:
- Proxmox operating system
- Active VM operating systems
- Frequently accessed workloads

### HDD

Used for:
- File server data
- VM backups
- Bulk storage
- Less performance-sensitive workloads

## Network

Home network:

`192.168.50.0/24`

Lab network:

`192.168.10.0/24`

The lab network is isolated behind OPNsense.

## Active Directory

- Domain: `ad.home.arpa`
- NetBIOS: `HOME`
- Domain controller: `WINDC-01`
- DNS: `192.168.10.10`

## Current State

The lab currently provides:

- Active Directory
- DNS
- Group Policy
- Windows domain authentication
- Isolated virtual networking
- Firewall/NAT
- Windows file server infrastructure
