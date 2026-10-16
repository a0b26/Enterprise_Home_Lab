# OPNsense Firewall

## Purpose

OPNsense provides routing and firewalling for the isolated Home Lab network. It acts as the default gateway for lab VMs outbound source NAT to the home router.

This document records the OPNsense implementation. For the broader network design and IP plan, see:

- [Network Topology](../architecture/network-topology.md)
- [IP Addressing](../architecture/ip-addressing.md)
- [Design Decisions](../architecture/design-decisions.md)

## Virtual Machine

| Setting | Configuration |
|---|---|
| VM name | `OPNsense-01` |
| VM ID | `102` |
| vCPU | 2 |
| Memory | 2 GB |
| Virtual disk | 16 GB |
| WAN virtual NIC | Proxmox `net0` → `vmbr0` → OPNsense `vtnet0` |
| LAN virtual NIC | Proxmox `net1` → `vmbr1` → OPNsense `vtnet1` |

The VM connects to two different Proxmox bridges. `vmbr0` connects the WAN interface to the home network, while `vmbr1` is a virtual bridge for the lab network and has no physical network port attached. 
* This arrangement is intended to keep lab guests separate from the home LAN whilst allowing controlled outbound connectivity through OPNsense. 

## Interface Configuration

| Interface | Role | Addressing | Notes |
|---|---|---|---|
| `vtnet0` / WAN | Upstream connection | DHCP from home network | The upstream gateway has been `192.168.50.1`. Confirm the current lease and gateway in OPNsense. |
| `vtnet1` / LAN | Lab gateway | Static `192.168.10.1/24` | Default gateway for lab VMs. |

## Routing and DNS

- Lab systems use `192.168.10.1` as their default gateway.
- Domain joined Windows clients use the domain controller (`192.168.10.10`) for DNS rather than using an external DNS server directly.
- The domain controller forwards external DNS queries to the OPNsense LAN address (`192.168.10.1`).

This keeps Active Directory name resolution under the domain controller's control whilst allowing external names to be resolved. 

## Related Configuration

- [Firewall Rules](firewall-rules.md)
- [Source NAT](nat.md)
- [Future VLANs](future-vlans.md)

## Validation Checklist

Record the date and result when each check is performed.

- [x] OPNsense WAN receives an address and has an online upstream gateway - **18/08/2026**
- [x] OPNsense can reach the home router and an external IP address - **18/08/2026**
- [x] Lab guests can reach `192.168.10.1` - **18/08/2026**
- [x] Lab guests can reach an external IP address when the intended firewall and NAT rules are enabled - **18/08/2026**
- [x] Domain-joined clients can resolve internal Active Directory names using the domain controller - **17/08/2026**
- [x] Domain-joined clients can resolve external names through the domain controller's configured forwarder - **18/08/2026**
- [ ] No unintended inbound access from the home network or WAN to lab guests is permitted - **To be tested**

## Troubleshooting Notes

When a lab guest cannot reach the internet, steps I would take would be as follows:

1. Confirm the guest has the expected IP address, subnet mask, default gateway and DNS server.
2. Test connectivity to the OPNsense LAN address (`192.168.10.1`).
3. Test an external IP address to distinguish routing/NAT problems from DNS problems - e.g. `1.1.1.1`.
4. Test DNS resolution separately and confirm the guest is using the domain controller for DNS.
5. Review the relevant OPNsense firewall logs and rule counters.
6. Check the Source NAT rule and the OPNsense WAN gateway status.

* Issues will be reported in the troubleshooting section of the Home Lab documentation.

## References

- [OPNsense Interface Configuration](https://docs.opnsense.org/manual/interfaces.html)
- [OPNsense Firewall Rules](https://docs.opnsense.org/manual/firewall.html)
- [OPNsense Network Address Translation](https://docs.opnsense.org/manual/nat.html)
