
---

# `docs/infrastructure/virtual-networking.md`

```md
# Virtual Networking

This document records the virtual networking configuration used in the SBXQIAO Enterprise Lab.

---

## Virtual Switch Overview

Three Hyper-V virtual switches are used.

| Switch | Type | Purpose |
|------|------|------|
| vSwitch-WAN | External | Internet / upstream connectivity |
| vSwitch-SBX | Internal | SBX site LAN |
| vSwitch-SBY | Internal | SBY site LAN |

---

## External Network

`vSwitch-WAN` connects the lab environment to the upstream home network.

Connected systems:

- pfSense-A
- pfSense-B

Purpose:

- Allow firewalls to access the internet
- Allow package downloads and updates

---

## Internal Networks

Internal switches isolate the lab networks from the host network.

### SBX Network

Subnet:

`172.16.50.0/24`

Gateway:

`172.16.50.1`

Connected systems:

| System | Role |
|------|------|
| pfSense-A | Gateway |
| SBX-DC1 | Domain controller |
| SBX-CL1 | Windows client |
| SBX-LX1 | Linux server |

---

### SBY Network

Subnet:

`172.16.60.0/24`

Gateway:

`172.16.60.1`

Connected systems:

| System | Role |
|------|------|
| pfSense-B | Gateway |
| SBY-DC1 | Domain controller |
| SBY-CL1 | Windows client |

---

## Traffic Flow

Example traffic path:

```text
Client
  │
SBX-CL1
  │
vSwitch-SBX
  │
pfSense-A
  │
vSwitch-WAN
  │
Internet
Network Design Goals

The virtual network is designed to provide:

Isolation from the home network

Controlled routing through firewalls

Simulated enterprise site separation

Flexible expansion for future services

Future Networking Enhancements

Possible improvements include:

VLAN segmentation

Dedicated management networks

Monitoring network segments

Bastion host access networks

Network traffic analysis