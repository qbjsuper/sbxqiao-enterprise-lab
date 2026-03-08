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
