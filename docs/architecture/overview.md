# Architecture Overview

This document provides a high-level summary of the SBXQIAO Enterprise Lab architecture.

---

## Purpose

The lab is designed to simulate a small enterprise environment for learning and practicing infrastructure engineering skills.

Primary focus areas include:

- Active Directory
- Virtual networking
- Firewall and routing
- Multi-site design
- VPN connectivity
- Windows and Linux server administration

---

## Design Principles

The lab is built using the following principles:

- Keep the environment isolated from production and home services
- Use repeatable VM deployment through templates
- Document decisions clearly
- Build in stages from simple to more realistic
- Prefer operational clarity over unnecessary complexity

---

## Current Scope

The current lab scope includes:

- One Hyper-V host
- Multiple internal virtual switches
- Two logical lab sites
- pfSense virtual firewalls
- Windows Server and Windows client virtual machines
- Ubuntu Server virtual machines
- A single Active Directory forest and domain

---

## Hypervisor Platform

The environment runs on:

`Microsoft Hyper-V`

Host hardware:

| Component | Specification |
|---|---|
| Device | Minisforum MS-A2 |
| CPU | AMD Ryzen 9 9955HX |
| RAM | 64 GB |
| Storage | 2 TB NVMe |
| NICs | 2 × 2.5G + 2 × 10G |

Current design decision:

- Use one physical NIC for all traffic for the initial phase

---

## Identity Architecture

Active Directory design:

| Item | Value |
|---|---|
| Forest | `sbxqiao.lab` |
| Domain | `sbxqiao.lab` |
| Sites | `SBX`, `SBY` |

This is a single-forest, single-domain, multi-site design.

---

## Logical Site Layout

### SBX Site

Primary lab site used for initial deployment.

Planned systems:

- `SBX-DC1`
- `SBX-CL1`
- `SBX-LX1`
- `pfSense-A`

### SBY Site

Secondary lab site for later expansion.

Planned systems:

- `SBY-DC1`
- `SBY-CL1`
- `pfSense-B`

---

## Deployment Strategy

The lab is being built in controlled stages:

1. Hypervisor and storage foundation
2. Template factory
3. Virtual network fabric
4. First site deployment
5. Active Directory services
6. Site-to-site connectivity
7. Multi-site services and testing

---

## Current Status

Completed:

- Hyper-V setup
- Base virtual switch design
- Template VM factory
- Initial architecture planning

Next major milestone:

- Deploy the first live site: `SBX`

---

## Site Model

The lab simulates two enterprise locations.

### Site SBX

Primary infrastructure site hosted on the main Hyper-V workstation.

Subnet:

172.16.50.0/24

Core systems:

- SBX-RTR1 (pfSense)
- SBX-DC1 (Domain Controller)
- SBX-CL1 (Windows Client)
- SBX-LX1 (Linux Server)

### Site SBY (Planned)

Secondary site hosted on a separate mini PC.

Subnet:

172.16.60.0/24

Planned systems:

- pfSense-B
- SBY-DC1 (Additional Domain Controller)
- SBY-CL1 (Client workstation)

The SBY site will simulate a remote office connected via a site-to-site VPN.
