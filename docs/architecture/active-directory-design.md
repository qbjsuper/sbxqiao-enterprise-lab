# `docs/architecture/active-directory-design.md`

```md
# Active Directory Design

This document defines the Active Directory architecture used in the SBXQIAO Enterprise Lab.

The environment simulates a small enterprise Active Directory deployment with multiple sites.

---

## Forest Structure

The lab uses a single Active Directory forest.

| Item | Value |
|-----|------|
| Forest Name | sbxqiao.lab |
| Domain Name | sbxqiao.lab |
| Domain Type | Single Domain |
| Functional Level | Windows Server 2025 |

The design follows a **single forest / single domain / multi-site architecture**.

---

## Domain Controllers

### SBX Site

The first domain controller is deployed in the primary site.

| Server | Role |
|------|------|
| SBX-DC1 | Primary Domain Controller |

Responsibilities:

- Active Directory Domain Services
- DNS
- Authentication
- Directory services

---

### SBY Site

A secondary domain controller will be deployed later.

| Server | Role |
|------|------|
| SBY-DC1 | Secondary Domain Controller |

This server will provide:

- Authentication redundancy
- Local authentication for SBY
- Active Directory replication

---

## FSMO Roles

Initially, all FSMO roles reside on:
SBX-DC1

FSMO roles include:

| Role | Description |
|----|----|
| Schema Master | Controls schema modifications |
| Domain Naming Master | Manages domain additions |
| RID Master | Allocates security identifiers |
| PDC Emulator | Handles time sync and password authority |
| Infrastructure Master | Maintains cross-domain references |

---

## Organizational Unit Structure

Initial OU layout:

```text
SBXQIAO
│
├── Domain Controllers
├── Servers
├── Workstations
└── Users
Example placements:

OU	Objects
Domain Controllers	SBX-DC1
Servers	Linux servers, infrastructure services
Workstations	Windows client machines
Users	Test user accounts
DNS Configuration

Active Directory integrated DNS will be used.

Primary zone:
sbxqiao.lab
DNS responsibilities:

Domain name resolution

Service discovery

Active Directory location records

Example record:

_ldap._tcp.dc._msdcs.sbxqiao.lab
Authentication Process

Typical domain login sequence:

Client boots and receives network configuration.

Client contacts DNS server.

DNS returns the domain controller location.

Client sends authentication request.

Domain controller validates credentials.

Replication Strategy

Once multiple domain controllers exist, Active Directory will replicate between sites.

Replication path:

SBX-DC1 ⇄ SBY-DC1

Replication will occur through the VPN tunnel between sites.

Future Active Directory Features

The lab environment may later include testing for:

Group Policy management

Organizational unit delegation

Active Directory replication troubleshooting

Read-only domain controllers

Certificate services

Identity federation