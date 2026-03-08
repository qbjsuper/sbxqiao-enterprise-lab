# SBXQIAO Enterprise Infrastructure Lab

Enterprise-style homelab designed to simulate real-world infrastructure environments.

This project documents the design, deployment, and operation of a multi-site enterprise network using virtualization and open-source networking technologies.

---

## Project Goals

The purpose of this lab is to develop practical experience with enterprise infrastructure systems, including:

- Active Directory domain architecture
- Multi-site network topology
- Firewall and routing with pfSense
- Site-to-site VPN connectivity
- Windows and Linux server administration
- Infrastructure documentation and change tracking

This environment is designed to mirror the architecture and operational patterns commonly used in enterprise networks.



## Virtual Network Architecture

```text
          Internet
             │
        vSwitch-WAN
        │          │
     pfSense-A   pfSense-B
        │          │
     vSwitch-SBX  vSwitch-SBY
        │          │
     SBX Site     SBY Site

--- 
## Lab Architecture

The SBXQIAO Enterprise Lab simulates a small multi-site enterprise environment.

```mermaid
graph TD

Internet --> WAN

WAN --> pfSenseA
WAN --> pfSenseB

pfSenseA --> SBX
pfSenseB --> SBY

SBX --> SBX_DC1
SBX --> SBX_CL1
SBX --> SBX_LX1

SBY --> SBY_DC1
SBY --> SBY_CL1
