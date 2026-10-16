# Proxmox VE Host

## Purpose

This document describes the Proxmox configuration supporting the Home Lab's virtual infrastructure.

## Hypervisor Role

Proxmox provides the virtualisation platform for the Home Lab which hosts all of the current Virtual Machines.

The environment is designed to simulate a small enterprise network whilst operating within the resource constraints of older hardware.

## Virtualisation Configuration

Virtual machines use KVM based virtualisation, with virtual hardware selected according to the guest operating system's requirements and the capabilities of the physical host.

VirtIO devices are used where appropriate to provide paravirtualised storage and networking.

## Network Configuration

Proxmox uses virtual network bridges to connect virtual machines to the relevant network segments.

- `vmbr0`: Connected to the physical/home network. Used for Proxmox host connectivity and the OPNsense WAN interface.
- `vmbr1`: An isolated virtual network used for the laboratory network and the OPNsense LAN interface.


Refer to [Network Topology](../architecture/network-topology.md) for the network diagram and [IP Addressing](../architecture/ip-addressing.md) for device addresses.

## Resource Constraints

The host has 12 GB of physical RAM, limiting the number of virtual machines that can operate simultaneously.

Resource allocation is prioritised according to each VM's role and some workloads are shut down when not required.

## Management and Maintenance

Proxmox is administered through its web interface over HTTPS.

Host maintenance has allowed me to:

- Monitor CPU and memory utilisation.
- Check storage capacity and health.
- Manage virtual machines.
- Maintain VM backups.
- Apply appropriate updates.
- Verify that VMs can be restored from backup.

## Limitations

- Limited physical memory restricts simultaneous workloads.
- The older CPU could cause compatibility issues with Guest OSes in the future
- Whilst the host and its storage devices represent potential single points of failure, the environment is intended for learning and testing not production workloads.

## Future Improvements

- Improve backup redundancy.
- Expand network segmentation.
- Introduce centralised logging and monitoring.
