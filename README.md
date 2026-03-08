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

---

## Hardware Platform

Host system used for the lab:

| Component | Specification |
|----------|---------------|
| Device | Minisforum MS-A2 |
| CPU | AMD Ryzen 9 9955HX |
| RAM | 64 GB |
| Storage | 2 TB NVMe |
| Network Interfaces | 2 × 2.5G + 2 × 10G |

Hypervisor platform:

Microsoft Hyper-V

---

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