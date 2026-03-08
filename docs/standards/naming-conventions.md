# Naming Conventions

This document defines naming standards for infrastructure components.

---

## Virtual Machines

Pattern:
[SITE]-[ROLE][NUMBER]

Example:

| Name | Description |
|-----|-----|
| SBX-DC1 | Domain Controller |
| SBX-CL1 | Windows Client |
| SBX-LX1 | Linux Server |
| SBY-DC1 | Secondary Domain Controller |

---

## Sites

| Code | Description |
|-----|-----|
| SBX | Primary lab site |
| SBY | Secondary lab site |

---

## Network Devices

| Name | Role |
|-----|-----|
| pfSense-A | Firewall for SBX |
| pfSense-B | Firewall for SBY |