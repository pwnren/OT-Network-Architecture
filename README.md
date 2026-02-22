# Purdue Model OT Network Segmentation Architecture
Reference OT network architecture aligned with the Purdue Model. Includes segmentation strategy, DMZ design, secure remote access, tiered administration, and Layer 2/3 design patterns to support secure, highly available industrial control system environments.

The objective is to demonstrate:
- Secure OT/IT segmentation
- Industrial DMZ (Level 3.5) implementation
- VLAN and VRF separation
- Controlled access enforcement between levels
- Least privilege communication flows
- OT focused network hardening practices
- High availability design considerations

This project reflects real-world industrial and manufacturing network architecture patterns.

## Architecture Summary
| Level | Function              | VLAN | Subnet            | Usable IPs |
|-------|-----------------------|------|------------------ |------------|
| 5     | Enterprise IT         | 10   | 10.10.10.0/24     | 254        |
| 3     | Operations            | 20   | 10.10.20.0/24     | 254        |
| 3.5   | Industrial DMZ        | 35   | 10.10.35.0/26     | 62         |
| 2     | HMI / Supervisory     | 40   | 10.10.40.0/27     | 30         |
| 1     | PLC / Control         | 50   | 10.10.50.0/28     | 14         |

- Each production area receives its own VLAN and subnet
- Segmentation aligns with Purdue Model layering
- Subnet sizing follows device density requirements per level
- Default gateway resides at the routed boundary (Layer 3 SVI / firewall)
- Inter zone traffic is controlled via ACLs/firewall policy
- No direct IT to OT routing without defined security policy

---

## 🔐 Supporting Security Baseline

This architecture is reinforced by a hardened Cisco IOS configuration baseline designed specifically for Operational Technology environments.

➡️ [Cisco IOS Secure Baseline – OT Focused](https://github.com/pwnren/Cisco-IOS-Secure-Baseline-Hardening)

The baseline includes:

- Management plane protection
- TACACS+ AAA enforcement
- SSHv2 & SNMPv3 hardening
- Layer 2 protection controls (BPDU Guard, Root Guard, UDLD)
- VRF segmentation support
- Defense in depth configuration standards

---


## Security Design Principles
- Default-deny between Enterprise IT and OT zones
- No direct Level 1 to Level 5 communication
- All IT to OT administrative access traverses Level 3.5 (Industrial DMZ)
- East to West traffic minimized within OT zones
- Segmentation enforced using VLANs, VRFs, ACLs, and firewall policies
- Tiered administration via designated jump hosts
- Management plane isolation from control traffic

## Layer 2 & Layer 3 Design Patterns
- Rapid PVST for loop prevention
- BPDU Guard, Root Guard, and Loop Guard enforcement
- LACP based EtherChannel for uplink resiliency
- VRF separation between BUSINESS, OPERATIONS, IDMZ, and OT domains
- Static routing or firewall mediated inter-zone routing
- IP SLA tracking for failover validation (future enhancement)

##  Key Controls Implemented
- VLAN based segmentation aligned to Purdue levels
- VRF separation for domain isolation
- Inter-VLAN ACL enforcement
- Port security on access layer
- BPDU Guard enabled on edge ports
- Disabled unused services (CDP, HTTP server)
- SNMPv3 recommended for production
- Logging and monitoring hooks for SIEM integration

## Example Traffic Flow Policy

| Source | Destination | Allowed | Notes |
|--------|------------|---------|-------|
| IT | PLC | ❌ | Blocked |
| IT | IDMZ Jump Host | ✅ | HTTPS only |
| IDMZ | HMI | ✅ | RDP only |
| HMI | PLC | ✅ | Modbus/TCP (502) |
| PLC | Internet | ❌ | Blocked |
| OT | Domain Controller | ⚠ | Controlled authentication only |
