Network Troubleshooting by OSI Model (Layer 1–7)

A structured troubleshooting methodology aligned with the OSI model to isolate faults quickly in enterprise and OT environments.

## Layer 1 – Physical
Transmits raw bits over physical medium
- Check cables, fiber, connectors
- Verify link light
- Confirm speed/duplex match
- Use cable tester

Common issues:
- Bad cable
- Mismatched duplex
- Unplugged interface
- Damaged fiber

## Layer 2 – Data Link
Switching, MAC addressing, VLAN tagging

Common causes:
- Wrong VLAN assignment
- Trunk not allowing VLAN
- Spanning Tree blocking port
- Port security violation
- BPDU Guard shutdown
- MAC address table issues

Useful commands:

```bash
show vlan brief
show interfaces trunk
show spanning-tree
show mac address-table
```

## Layer 3 – Network
IP addressing, routing, gateway logic

Validate:
- Correct IP address
- Correct subnet mask
- Default gateway configured
- Gateway reachable (ping)
- Routing table accuracy
- VRF assignment correct

Useful commands:
```bash
ping <gateway>
show ip route
traceroute <destination>
show ip interface brief
```

## Layer 4 – Transport (TCP/UDP)
Port-based communication

Common causes:
- TCP/UDP port not listening
- Firewall or ACL blocking
- NAT misconfiguration
- Wrong service port

Testing tools:
```bash
telnet <ip> <port>
Test-NetConnection (PowerShell)
netstat -an
```

## Layer 5 – Session
Maintains session state

Issues may include:
- Authentication sessions dropping
- VPN timeout issues
- RDP session instability
- Firewall session table exhaustion
- Token expiration

Check:
- VPN logs
- RDP logs
- Firewall session table
- Authentication server logs

## Layer 6 – Presentation
Encryption & data formatting

Common issues:
- SSL/TLS certificate mismatch
- Expired certificates
- Protocol version mismatch
- Cipher mismatch

Symptoms:
- HTTPS works but shows certificate error
- Secure connection fails unexpectedly

## Layer 7 – Application

Access to application services

Validate:
- DNS resolution
- Application service running
- HTTP 500 / 404 errors
- Timeout errors
- Proxy misconfiguration
- Load balancer misrouting

Commands:

nslookup
dig
curl -v https://google.com

# Troubleshooting OSI Layer
| Test                | Likely Layer |
| ------------------- | ------------ |
| Cannot ping device  | L1–L3        |
| Cannot ping gateway | L2–L3        |
| Cannot ping DNS     | L3           |
| DNS won’t resolve   | L7           |
| Port closed         | L4           |
| SSL error           | L6           |
| Login/session issue | L5–L7        |


# Troubleshooting Decision Tree

  START
                   │
                   ▼
        1️⃣  Ping Device IP?
                   │
        ┌──────────┴──────────┐
        │                     │
      ❌ No                  ✅ Yes
  L1–L3 Issue          Continue ▼
                             
                   2️⃣ Ping Default Gateway?
                   │
        ┌──────────┴──────────┐
        │                     │
      ❌ No                  ✅ Yes
   Likely L2/L3        Continue ▼
                             
                   3️⃣ Ping DNS Server?
                   │
        ┌──────────┴──────────┐
        │                     │
      ❌ No                  ✅ Yes
     L3 Issue           Continue ▼
                             
                   4️⃣ Resolve DNS Name?
                   │
        ┌──────────┴──────────┐
        │                     │
      ❌ No                  ✅ Yes
  L7 (DNS Service)     Continue ▼
                             
                   5️⃣ Port Test (e.g., 443)?
                   │
        ┌──────────┴──────────┐
        │                     │
      ❌ Fails              ✅ Open
     L4 Issue           Continue ▼
                             
                   6️⃣ HTTPS Loads?
                   │
        ┌──────────┴──────────┐
        │                     │
      ❌ SSL Error           ✅ Yes
       L6 Issue         Continue ▼
                             
                   7️⃣ Login Works?
                   │
        ┌──────────┴──────────┐
        │                     │
      ❌ No                 ✅ Yes
    L5–L7 Issue        Application OK
