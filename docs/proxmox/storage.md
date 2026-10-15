# Proxmox Storage Architecture

## Purpose

This document describes the storage layout used by Proxmox, including VM operating system disks, data volumes and backup destinations.

## Physical Storage

| Device | Approximate Capacity | Intended Role |
|---|---|---|
| Primary SSD | 250 GB | Proxmox host and active VM storage |
| Secondary HDD | 750 GB | Additional VM storage, data and backups |

## Proxmox Storage Configuration

| Storage ID | Type | Intended Purpose |
|---|---|---|
| `local` | Directory | ISO images, templates and other supported file based content |
| `local-lvm` | LVM thin | Virtual machine disks |
| `backup` | LVM thin | Additional storage, potentially backed by the secondary HDD |

## Virtual Machine Disk Layout

VM operating system disks are stored on the primary SSD where practical, whilst selected data volumes use the secondary HDD.

The File Server uses the SSD for its boot disk but has a separate volume on the HDD for file share data.

| VM | Disk | Intended Use | Storage |
|---|---|---|---|
| `WINDC-01` | 60 GB | Windows Server operating system | `local-lvm` |
| `WIN11-01` | 40 GB | Windows 11 operating system | `local-lvm` |
| `OPNsense-01` | 16 GB | Firewall operating system | `local-lvm` |
| `FILESRV-01` | 40 GB | Windows Server operating system | `local-lvm` |
| `FILESRV-01` | 60 GB | File share data | `backup` |

The purpose of this separation is to keep frequently accessed operating system disks on the faster and more reliable SSD whilst using the HDD for additional capacity.

## Backup Strategy

VM backups are stored separately from active VM disks.

The secondary HDD offers additional storage capacity, but it is still within the same physical host. A major failure to the host could potentially compromise the backup.

Snapshots can provide convenient rollback points before configuration changes. though these are not a substitute for proper backups.

## Future Improvements

- Establish a documented backup schedule and retention policy.
- Maintain an additional backup copy on separate device(s).
- Test restoring a VM from the backup.
- Record storage utilisation and capacity estimates/thresholds.
