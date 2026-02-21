# Power-of-Two Method + OT 

🔹 The /24 Anchor Method

`/24 = 256` total IP addresses

From there, everything is just:

- ➗ **Divide by 2** (Going to larger prefix numbers / more specific subnets)  
  `/25 → /26 → /27 → /28 → /29 → /30`

- ✖ **Multiply by 2** (Going to smaller prefix numbers / larger networks)  
  `/23 → /22 → /21 → /20 → /19`

Subnetting = **Powers of 2**.

---

## 📊 Host Capacity Reference Table

### ➗ Divide by 2 (More Specific Subnets)

| Prefix | Subnet Mask       | Total IPs | Usable Hosts |
|-------:|-------------------|----------:|-------------:|
| /24 | 255.255.255.0   | 256 | 254 |
| /25 | 255.255.255.128 | 128 | 126 |
| /26 | 255.255.255.192 | 64  | 62  |
| /27 | 255.255.255.224 | 32  | 30  |
| /28 | 255.255.255.240 | 16  | 14  |
| /29 | 255.255.255.248 | 8   | 6   |
| /30 | 255.255.255.252 | 4   | 2   |
| /31 | 255.255.255.254 | 2   | 2 (P2P) |
| /32 | 255.255.255.255 | 1   | 1   |

### ✖ Multiply by 2 (Larger Networks)

| Prefix | Subnet Mask       | Total IPs |
|-------:|-------------------|----------:|
| /24 | 255.255.255.0   | 256 |
| /23 | 255.255.254.0   | 512 |
| /22 | 255.255.252.0   | 1024 |
| /21 | 255.255.248.0   | 2048 |
| /20 | 255.255.240.0   | 4096 |
| /19 | 255.255.224.0   | 8192 |
| /18 | 255.255.192.0   | 16384 |
| /17 | 255.255.128.0   | 32768 |
| /16 | 255.255.0.0     | 65536 |
---

## 🔥 Block Size Method (Fast Mental Subnetting)

**Formula:** `Block Size = 256 − Interesting Octet`

**Example:**  
`/26 = 255.255.255.192`  
`256 − 192 = 64`

**Subnet increments:** `0, 64, 128, 192`

---

## ⚡ Powers of Two (Memorize This Row)

`256 128 64 32 16 8 4 2 1`

All subnet math comes from this sequence.

---

## 🧱 Octet Boundaries (Know Cold)

| Prefix | Subnet Mask |
|-------:|-------------|
| /8  | 255.0.0.0 |
| /16 | 255.255.0.0 |
| /24 | 255.255.255.0 |

Everything else is derived between these boundaries.

---

## 🧮 Address Formula

`2^(32 − prefix) = Total Addresses`

**Example:** `/27`  
`32 − 27 = 5` → `2^5 = 32 addresses`

# 🏭 OT-Specific Subnet Design
---

## Level 5 – Enterprise IT

**Typical Size:** `/22` or `/23`  
**Example Capacity:**
- `/23` = 512 IPs  
- `/22` = 1024 IPs  

**Why:**
- User devices
- Application servers
- Higher host density
- Standard enterprise broadcast tolerance

---

## Level 3 – Operations / Industrial DMZ

**Typical Size:** `/26` or `/27`

**Why:**
- Historians
- Jump hosts
- Patch servers
- Controlled cross-zone access
- Smaller broadcast domain
- Tighter segmentation boundaries

---

## Level 2 – HMI / Supervisory

**Typical Size:** `/27` or `/28`

**Why:**
- HMIs
- Engineering workstations
- SCADA supervisory nodes
- Moderate device count
- Reduced lateral movement risk

---

## Level 1 – PLC / Control Devices

**Typical Size:** `/28` or `/29`

**Example Capacity:**
- `/28` = 16 IPs (14 usable)
- `/29` = 8 IPs (6 usable)

**Why:**
- Small fixed device count
- Deterministic communications
- Minimize broadcast domain
- Reduce attack surface
- Contain failure scope

---

## Infrastructure / Transit Networks

**Typical Size:** `/30` or `/31`

**Use Cases:**
- Router uplinks
- Firewall transit VLANs
- Core-to-distribution links
- OT zone boundaries

`/31` recommended for point-to-point links (RFC 3021)

---

## 🔐 OT Design Principles

- Right-size VLANs (do not oversize Level 1/2)
- Smaller broadcast domains reduce outage scope
- Align subnets with trust boundaries
- Enforce policy at Layer 3 or firewall boundary
- Default-deny between Purdue levels
- Separate management plane where possible

---
