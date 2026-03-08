# IP Addressing Plan

This document defines the IP addressing scheme used in the lab environment.

---

## SBX Network

Network:
172.16.50.0 /24

| Device | IP |
|------|------|
| Gateway (pfSense-A) | 172.16.50.1 |
| SBX-DC1 | 172.16.50.10 |
| Clients | 172.16.50.100 - 172.16.50.200 |

---

## SBY Network

Network:
172.16.60.0 /24

| Device | IP |
|------|------|
| Gateway (pfSense-B) | 172.16.60.1 |
| SBY-DC1 | 172.16.60.10 |
| Clients | 172.16.60.100 - 172.16.60.200 |

---
# Network Address Plan

## SBX Site

Subnet: 172.16.50.0/24

| Host | Address |
|-----|------|
| SBX-RTR1 | 172.16.50.1 |
| SBX-DC1 | 172.16.50.10 |
| SBX-CL1 | 172.16.50.20 |
| SBX-LX1 | 172.16.50.30 |

## SBY Site (Planned)

Subnet: 172.16.60.0/24

| Host | Address |
|-----|------|
| pfSense-B | 172.16.60.1 |
| SBY-DC1 | 172.16.60.10 |
| SBY-CL1 | 172.16.60.20 |
