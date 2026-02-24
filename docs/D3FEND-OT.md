# MITRE D3FEND – OT 

This architecture defensive techniques defined in the MITRE D3FEND OT domain.

Official References:
- MITRE D3FEND OT Domain: https://d3fend.mitre.org/domain/ot/
- MITRE D3FEND Framework: https://d3fend.mitre.org/

MITRE D3FEND provides a defensive knowledge graph that maps countermeasures to system artifacts and adversary behaviors. The OT domain extends this model to industrial control systems (ICS) and cyber to physical environments.

---

## D3FEND OT to Purdue Model 

| Purdue Level | Functional Area | Applied D3FEND OT Techniques |
|--------------|----------------|------------------------------|
| Level 5 | Enterprise IT | User Group Permissions, Change Default Password |
| Level 3.5 | Industrial DMZ | Directional Network Link, Remote Firmware Update Monitoring |
| Level 3 | Operations | Operational Process Monitoring, Platform Uptime Monitoring |
| Level 2 | HMI / Supervisory | Application Performance Monitoring, Application Exception Monitoring |
| Level 1 | PLC / Control | Operational Logic Validation, OT Variable Access Restriction |
| Physical Layer | Cabinets / Facilities | Physical Locking, Physical Access Mediation, Physical Enclosure Hardening |

---

## Defensive Control

| D3FEND OT Techniques Examples | Implementation |
|---------------------|------------------------------|
| Operational Logic Validation | PLC logic integrity controls and change management enforcement |
| Operating Mode Restriction | Restrict Run/Program mode transitions to authorized engineering workstations |
| Remote Firmware Update Monitoring | Alerting on unauthorized firmware update commands at boundary layers |
| OT Variable Access Restriction | Read/write control enforcement on controller registers and tags |
| Directional Network Link | One-way communication paths between OT and enterprise networks |
| Physical Locking | Secured control cabinets and restricted physical access |
| Hardware-based Write Protection | Write-protect controls on firmware and removable storage media |

---

## Threat Defensive Objectives

This supports mitigation of:

- Unauthorized PLC logic modification
- Malicious firmware deployment
- Unauthorized controller mode transitions
- Lateral movement into control networks
- Physical tampering of industrial systems
- Unsafe process state manipulation

---

All D3FEND terminology and framework concepts are attributed to MITRE.

## Attribution

MITRE D3FEND™ is a trademark of The MITRE Corporation.

This project references publicly available information from the MITRE D3FEND OT domain (https://d3fend.mitre.org/domain/ot/) for educational and alignment purposes only.

MITRE does not endorse this project.
