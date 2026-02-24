# OT Network Protocol Troubleshooting Reference Guide

---

## EtherNet/IP (CIP)

| Check | What to Validate | Commands |
|---|---|---|
| Connectivity | Layer 2/3 reachability between PLC and HMI/SCADA | `ping`, `arp -a` |
| Port Access | TCP/UDP **44818** open | `netstat`, firewall rules |
| Multicast | IGMP snooping configured | Switch IGMP tables |
| VLAN | Correct VLAN assignment | `show vlan brief` |
| QoS | Prioritization for control traffic | `show policy-map interface` |

**Common Issues**

- PLC not reachable  
- Produced/Consumed tag failures  
- Scanner timeouts  
- Multicast flooding  

---

## Modbus TCP

| Check | What to Validate | Commands |
|---|---|---|
| Port | TCP **502** reachable | `telnet <ip> 502` |
| Addressing | Correct unit ID/register mapping | Verify device config |
| Latency | Response delays/timeouts | Packet capture |
| Firewall | ACL blocking port 502 | Firewall logs |

**Common Issues**

- Incorrect register mapping  
- Timeout due to latency  
- NAT breaking sessions  

---

## PROFINET

| Check | What to Validate | Commands |
|---|---|---|
| VLAN Priority | Real-time traffic priority | QoS configuration |
| Multicast | DCP discovery working | Packet capture |
| Device Name | Correct device naming | Engineering tool |
| Topology | LLDP neighbors visible | `show lldp neighbors` |

**Common Issues**

- Device not discovered  
- Real-time communication jitter  
- Duplicate device names  

---

## DNP3

| Check | What to Validate | Commands |
|---|---|---|
| Port | TCP/UDP **20000** reachable | Firewall validation |
| Polling | Master polling intervals correct | SCADA configuration |
| Time Sync | Time drift between systems | NTP status |
| Authentication | Secure authentication enabled | Device configuration |

**Common Issues**

- Poll failures  
- Time drift alarms  
- Authentication mismatch  

---

## OPC UA

| Check | What to Validate | Commands |
|---|---|---|
| Port | TCP **4840** reachable | Connectivity tests |
| Certificates | Trust relationship valid | Certificate store |
| Encryption | Security policy alignment | OPC configuration |
| Session | Active sessions stable | Server logs |

**Common Issues**

- Certificate trust failures  
- Endpoint mismatch  
- Security policy mismatch  

---

## BACnet/IP

| Check | What to Validate | Commands |
|---|---|---|
| Port | UDP **47808** reachable | Firewall rules |
| Broadcast | BBMD configuration correct | Router configuration |
| Subnet | Same broadcast domain where required | VLAN configuration |
| Device ID | Unique device IDs | Controller configuration |

**Common Issues**

- Broadcast blocked across VLANs  
- Duplicate device IDs  
- BBMD misconfiguration  

---

## Network-Level Checks (Applies to All Protocols)

| Layer | Validation |
|---|---|
| Layer 1 | Link state, optics/cabling errors |
| Layer 2 | VLAN membership, trunking |
| Layer 3 | Routing, VRF segmentation |
| ACLs | Allowed ports/protocols |
| Latency | Industrial tolerance thresholds |
| Jitter | Real-time traffic sensitivity |
| Packet Loss | Interface drops/errors |

### Useful Commands

```bash
ping
traceroute
tcpdump
netstat
arp -a
show interface status
show mac address-table
show ip route
show access-lists
show spanning-tree
