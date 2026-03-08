# IP Address Plan

## Overview

This document defines the IPv4 addressing rules for the **SBXQIAO Enterprise Lab**.

The addressing plan is designed to be:

- predictable
- scalable
- easy to troubleshoot
- aligned with real enterprise infrastructure practices

Each site is assigned its own subnet to support routing, VPN connectivity, and Active Directory site design.

---

# 1. Addressing Model

The lab uses the private IPv4 range:

172.16.0.0/16

Each site receives a dedicated `/24` subnet.

| Site | Subnet |
|-----|------|
| SBX | 172.16.50.0/24 |
| SBY | 172.16.60.0/24 |

This ensures:

- no network overlap
- clean VPN routing
- clear site separation

---

# 2. Subnet Layout

Each subnet uses the following structure.

| Address Range | Purpose |
|---------------|--------|
| .1 | Gateway / firewall |
| .2 – .9 | Reserved infrastructure |
| .10 – .19 | Domain controllers / core services |
| .20 – .29 | Windows member servers |
| .30 – .39 | Linux / utility servers |
| .40 – .49 | Management / jump hosts |
| .50 – .199 | DHCP client pool |
| .200 – .239 | Reserved for future infrastructure |
| .240 – .254 | Temporary lab testing |

This convention allows engineers to identify system roles directly from the IP address.

---

# 3. SBX Site Address Plan

Network:

172.16.50.0/24

Gateway:

172.16.50.1

### Core Infrastructure

| Host | Role | IP |
|-----|-----|-----|
| SBX-PFSENSE-A | Firewall / gateway | 172.16.50.1 |
| SBX-DC1 | Domain Controller | 172.16.50.10 |
| SBX-DC2 | Domain Controller (future) | 172.16.50.11 |

### Servers

| Host | Role | IP |
|-----|-----|-----|
| SBX-SRV1 | Windows server | 172.16.50.20 |
| SBX-LX1 | Linux server | 172.16.50.30 |

### Management

| Host | Role | IP |
|-----|-----|-----|
| SBX-JMP1 | Admin / jump workstation | 172.16.50.40 |

### DHCP Scope

172.16.50.50 – 172.16.50.199

Used for:

- domain clients
- temporary lab machines

---

# 4. SBY Site Address Plan

Network:

172.16.60.0/24

Gateway:

172.16.60.1

### Core Infrastructure

| Host | Role | IP |
|-----|-----|-----|
| SBY-PFSENSE-B | Firewall / gateway | 172.16.60.1 |
| SBY-DC1 | Domain Controller | 172.16.60.10 |

### Clients

| Host | Role | IP |
|-----|-----|-----|
| SBY-CL1 | Domain client | DHCP |

### DHCP Scope

172.16.60.50 – 172.16.60.199

---

# 5. DNS Configuration Rules

All domain-joined systems must use **Active Directory DNS servers**.

Example configuration:

SBX clients:

Primary DNS: 172.16.50.10

SBY clients:

Primary DNS: 172.16.60.10

Public DNS servers such as `8.8.8.8` should not be configured directly on domain members.

External DNS resolution should occur via:

- DNS forwarding on the domain controller
or
- firewall DNS forwarding

---

# 6. DHCP Rules

DHCP will be provided by the **Active Directory domain controller** at each site.

Infrastructure devices must use **static IP addresses**, including:

- firewalls
- domain controllers
- servers
- VPN endpoints

DHCP should only be used for:

- workstations
- temporary lab machines

---

# 7. VPN Routing Design

A site-to-site VPN will connect the two locations.

Traffic allowed across the VPN:

SBX: 172.16.50.0/24  
SBY: 172.16.60.0/24

Because the networks do not overlap, routing remains simple and predictable.

---

# 8. Expansion Strategy

Future sites should follow the same pattern.

| Site | Example Subnet |
|-----|-----|
| HQ | 172.16.70.0/24 |
| Cloud | 172.16.80.0/24 |
| Management | 172.16.90.0/24 |

---

# 9. Operational Rule

All new virtual machines must follow the addressing conventions defined in this document.

This prevents:

- IP conflicts
- inconsistent documentation
- DNS resolution issues
- routing problems
- VPN misconfiguration

---

## Current Approved Networks

SBX Site → 172.16.50.0/24  
SBY Site → 172.16.60.0/24
