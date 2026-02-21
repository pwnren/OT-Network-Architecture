# Power-of-Two Method + OT / Purdue Model Alignment

🔹 The /24 Anchor Method

/24 = 256 total IP addresses

From there, everything is just:

➗ Divide by 2
(Going to larger prefix numbers / more specific subnets)
/25 → /26 → /27 → /28 → /29 → /30

✖ Multiply by 2
(Going to smaller prefix numbers / larger networks)
/23 → /22 → /21 → /20 → /19

Subnetting = Powers of 2.

📊 Host Capacity Reference Table
➗ Divide by 2 (More Specific Subnets)
Prefix	Total IPs	Usable Hosts
/24	256	254
/25	128	126
/26	64	62
/27	32	30
/28	16	14
/29	8	6
/30	4	2
/31	2	2 (Point-to-Point)
/32	1	1

✖ Multiply by 2 (Larger Networks)
Prefix	Total IPs
/24	256
/23	512
/22	1024
/21	2048
/20	4096
/19	8192
/18	16384
/17	32768
/16	65536

🔥 Block Size Method (Fast Mental Subnetting)

Formula

Block Size = 256 − Interesting Octet

Example:

/26 = 255.255.255.192
256 - 192 = 64

Subnet increments:
0
64
128
192

That’s your subnet map.

⚡ Powers of Two (Memorize This Row)
256 128 64 32 16 8 4 2 1

All subnet math comes from this sequence.

🧱 Octet Boundaries (Know Cold)
Prefix	Subnet Mask
/8	255.0.0.0
/16	255.255.0.0
/24	255.255.255.0

Everything else is derived between these boundaries.

🧮 Address Formula
2^(32 − prefix) = Total Addresses

Example:
/27
32 − 27 = 5
2^5 = 32 addresses

🏭 OT-Specific Subnet Design
Level 5 – Enterprise IT

Typical Size: /22 or /23

Why: User devices, servers, higher host density

Example:
/23 = 512 IPs
/22 = 1024 IPs

🏭 Level 3 – Operations / Industrial DMZ

Typical Size: /26 or /27

Why: Controlled zone for historians, jump hosts, patch servers

Smaller broadcast domain

Tighter segmentation boundaries

🖥 Level 2 – HMI / Supervisory

Typical Size: /27 or /28

Why: Moderate device count (HMIs, engineering stations)

Reduced lateral movement risk

⚙ Level 1 – PLC / Control Devices

Typical Size: /28 or /29

Why:
- Small fixed device count
- Minimize broadcast domain
- Reduce attack surface

Example:

/28 = 16 IPs (14 usable)

/29 = 8 IPs (6 usable)

🔗 Point-to-Point Infrastructure Links

/30 = 2 usable hosts

/31 = 2 usable (RFC 3021, no broadcast)

Common for:

- Router uplinks
- Firewall transit VLANs
- Core-to-distribution links

🛡 OT Design Principles
- Right-size VLANs — do not oversize Level 1/2 networks
- Smaller broadcast domains reduce failure scope
- Align segmentation with trust boundaries
- Default deny between zones
Enforce policy at Layer 3 or firewall boundary
