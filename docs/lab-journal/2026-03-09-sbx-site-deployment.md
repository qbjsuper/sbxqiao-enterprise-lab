# Lab Journal – SBX Site Deployment

Date: 2026-03-09

---

## Objective

Begin deployment of the SBX site infrastructure.

Initial components to deploy:

- pfSense firewall
- Virtual network segments
- SBX domain controller

---

## Planned Infrastructure

Network Segments:

WAN
Connected to external network

LAN (SBX)
Internal Hyper-V network

Subnet plan:

172.16.50.0/24

Gateway:

172.16.50.1

---

## Planned Machines

SBX-PFS1
pfSense firewall

SBX-DC1
Primary domain controller

SBX-CL1
Windows workstation

SBX-LX1
Linux server

---

## Deployment Order

1. pfSense firewall
2. Internal network validation
3. Deploy SBX-DC1
4. Domain services validation