# Network Topology

This document describes the logical network architecture used in the SBXQIAO Enterprise Lab.

The lab simulates a small enterprise environment with two sites connected through firewall gateways.

---

## High-Level Topology

```text
                Internet
                   │
              Home Router
                   │
               vSwitch-WAN
                   │
        ┌──────────┴──────────┐
        │                     │
     pfSense-A             pfSense-B
        │                     │
     vSwitch-SBX           vSwitch-SBY
        │                     │
     SBX Site              SBY Site
     Each site has its own internal network and firewall gateway.

Virtual Switch Design

Three Hyper-V virtual switches are used in the lab.

Switch	Type	Purpose
vSwitch-WAN	External	Internet / upstream connectivity
vSwitch-SBX	Internal	SBX site LAN
vSwitch-SBY	Internal	SBY site LAN
WAN Segment

The WAN segment connects the virtual firewalls to the upstream home network.

Connected components:

System	Interface
pfSense-A	WAN
pfSense-B	WAN

This network provides:

Internet access

Software updates

Package downloads

SBX Site Network

The SBX site is the primary site of the lab.

Subnet:

172.16.50.0/24

Gateway:

172.16.50.1
Systems
System	Role
pfSense-A	Firewall / gateway
SBX-DC1	Domain controller
SBX-CL1	Windows client
SBX-LX1	Linux server
SBY Site Network

The SBY site represents a secondary branch office.

Subnet:

172.16.60.0/24

Gateway:

172.16.60.1
Systems
System	Role
pfSense-B	Firewall / gateway
SBY-DC1	Domain controller
SBY-CL1	Windows client
Traffic Flow Example

Typical internet traffic path:

SBX-CL1
   │
vSwitch-SBX
   │
pfSense-A
   │
vSwitch-WAN
   │
Home Router
   │
Internet
Planned Site-to-Site Connectivity

The two sites will eventually communicate through a VPN tunnel.

pfSense-A ⇄ IPsec VPN ⇄ pfSense-B

This will allow:

Active Directory replication

Cross-site authentication

Internal service communication

Design Goals

The network architecture is designed to:

Simulate enterprise site separation

Provide realistic routing paths

Allow firewall policy experimentation

Support VPN and multi-site services

Maintain isolation from the host network

Future Network Enhancements

The lab topology can later be expanded with:

VLAN segmentation

Management networks

Monitoring networks

Bastion host access

IDS / IPS systems

Network traffic analysis

---

## Multi-Site Architecture

The SBXQIAO sandbox is designed as a two-site enterprise simulation.

The two sites are hosted on separate physical Hyper-V hosts connected through a home router.

The router only provides Layer-2 transport and internet access.  
All lab networking is controlled by pfSense routers.

### Physical Layout

Internet  
↓  
Home Router / Switch  
↓  
Host A (Big PC – Hyper-V)  
Host B (Mini PC – Hyper-V)

### Logical Layout
              Internet
                 │
           Home Router
                 │
          ───── WAN ─────
            │         │
        pfSense-A   pfSense-B
           │           │
      SBX LAN       SBY LAN
    172.16.50.0     172.16.60.0


SBX and SBY represent two enterprise sites connected through a WAN transport network.

A site-to-site VPN will later connect the two LAN networks.

---
[2026-03-08 22:18 AEST]

Below is the **complete single Markdown file** version.
You can paste this directly into:

```
docs/network/network-topology.md
```

or keep it in:

```
docs/architecture/network-topology.md
```

Both are acceptable in infrastructure documentation.

---

```md
# Network Topology

## Overview

This document describes the logical network topology of the **SBXQIAO Enterprise Lab**.

The lab simulates a small multi-site enterprise infrastructure consisting of two locations:

- SBX Site
- SBY Site

Each site contains its own local network and infrastructure services.  
The sites will later be connected using a **site-to-site VPN** between two firewall systems.

---

# 1. High-Level Topology

```

Internet
│
vSwitch-WAN
│
├── pfSense-A
│      │
│      └── vSwitch-SBX (172.16.50.0/24)
│              │
│              ├── SBX-DC1
│              ├── SBX-CL1
│              └── SBX-LX1

└── pfSense-B
│
└── vSwitch-SBY (172.16.60.0/24)
│
├── SBY-DC1
└── SBY-CL1

```

Each site is isolated at Layer-2 using its own Hyper-V virtual switch.

---

# 2. Virtual Network Fabric

The environment uses **Hyper-V virtual switches** to represent network segments.

| Virtual Switch | Type | Purpose |
|---|---|---|
| vSwitch-WAN | External | Internet connectivity |
| vSwitch-SBX | Internal | SBX site LAN |
| vSwitch-SBY | Internal | SBY site LAN |

### WAN Network

The WAN switch connects both pfSense firewalls to the same simulated upstream network.

This allows:

- internet access
- VPN tunnel creation
- routing between sites

---

# 3. SBX Site Network

Subnet:

```

172.16.50.0/24

```

Gateway:

```

172.16.50.1

```

Gateway device:

```

SBX-PFSENSE-A

```

### Infrastructure

| Host | Role | IP |
|---|---|---|
| SBX-PFSENSE-A | Firewall / gateway | 172.16.50.1 |
| SBX-DC1 | Domain controller | 172.16.50.10 |
| SBX-CL1 | Domain client | DHCP |
| SBX-LX1 | Linux server | 172.16.50.30 |

### Services provided

- Active Directory Domain Services
- DNS
- DHCP
- Linux services (future)
- lab experimentation

---

# 4. SBY Site Network

Subnet:

```

172.16.60.0/24

```

Gateway:

```

172.16.60.1

```

Gateway device:

```

SBY-PFSENSE-B

```

### Infrastructure

| Host | Role | IP |
|---|---|---|
| SBY-PFSENSE-B | Firewall / gateway | 172.16.60.1 |
| SBY-DC1 | Domain controller | 172.16.60.10 |
| SBY-CL1 | Domain client | DHCP |

This site simulates a **secondary branch office**.

---

# 5. VPN Architecture

The two sites will be connected using **IPsec VPN**.

Connection:

```

SBX-PFSENSE-A ⇄ IPsec VPN ⇄ SBY-PFSENSE-B

```

Traffic allowed across the tunnel:

| Source | Destination |
|---|---|
| 172.16.50.0/24 | 172.16.60.0/24 |
| 172.16.60.0/24 | 172.16.50.0/24 |

This allows:

- Active Directory replication
- cross-site authentication
- remote access between sites

---

# 6. Active Directory Site Design

The environment uses a **single forest and single domain**.

Forest:

```

sbxqiao.lab

```

Domain:

```

sbxqiao.lab

```

Active Directory sites:

| AD Site | Network |
|---|---|
| SBX | 172.16.50.0/24 |
| SBY | 172.16.60.0/24 |

Each site has its own domain controller.

This simulates real enterprise deployments where branch offices maintain local authentication services.

---

# 7. Network Roles

### pfSense Firewalls

Responsibilities:

- routing
- NAT
- VPN gateway
- firewall policy enforcement

### Domain Controllers

Responsibilities:

- authentication
- DNS
- DHCP
- directory services

### Clients

Responsibilities:

- simulate enterprise workstation devices
- test domain join and authentication
- simulate user activity

---

# 8. Future Expansion

The network design allows additional sites to be added easily.

| Site | Subnet |
|---|---|
| HQ | 172.16.70.0/24 |
| Cloud | 172.16.80.0/24 |
| Management | 172.16.90.0/24 |

Each new site would follow the same architecture:

```

Firewall
│
Local subnet
│
Domain controller
│
Clients and servers

```

---

# 9. Design Goals

The topology is designed to simulate key enterprise networking concepts:

- multi-site Active Directory
- routed network segmentation
- firewall-based perimeter security
- VPN-based site connectivity
- centralized identity services

The environment provides a platform for practicing:

- system administration
- network administration
- infrastructure automation
- troubleshooting techniques
```

---





