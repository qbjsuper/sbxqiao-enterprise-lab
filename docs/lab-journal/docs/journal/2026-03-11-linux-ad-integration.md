# Lab Journal Entry

Date: 2026-03-11  
Stage: Linux Active Directory Integration  
Environment: SBXQIAO Enterprise Lab

---

# Objective

Integrate the Linux server (sbx-lx1) into the Active Directory domain and align it with the enterprise tiered administration model.

---

# Infrastructure Context

| Component | Value |
|----------|------|
| Domain | sbxqiao.lab |
| Domain Controller | sbx-dc1.sbxqiao.lab |
| DC IP | 172.16.50.10 |
| Linux Server | sbx-lx1 |
| Linux IP | 172.16.50.30 |
| Hypervisor | Hyper-V |
| Router | pfSense |

Network:


172.16.50.0/24


Gateway:


172.16.50.1


DNS:


172.16.50.10


---

# Active Directory Architecture

Tiered OU structure implemented.


SBX-T0
PrivilegedAccounts
DomainControllers

SBX-T1
JumpHosts
PrivilegedAccounts
Servers
SBX-LX1

SBX-T2
Workstations


Tier isolation enabled using:


Block Inheritance


This prevents domain-level policies from affecting tier-specific resources.

---

# Administrative Identity Model

Separate administrative identities created to enforce the tier model.


bojie.qiao.t0 → Tier 0 (Domain Admin)
bojie.qiao.t1 → Tier 1 (Server Admin)
bojie.qiao → Tier 2 (User)


Each account is placed in the correct OU:


SBX-T0 → PrivilegedAccounts
SBX-T1 → PrivilegedAccounts
SBX-T2 → Users


---

# Linux AD Integration

The Ubuntu server `sbx-lx1` was successfully integrated with Active Directory.

Authentication components used:


Kerberos
SSSD
realm join


Required packages installed:


sssd
sssd-tools
realmd
adcli
samba-common-bin
libnss-sss
libpam-sss
krb5-user


---

# Kerberos Verification

Authentication tested using:


kinit Administrator


Kerberos ticket verified:


klist


Result:

Kerberos authentication successfully issued a TGT from:


SBXQIAO.LAB


---

# Domain Join

Domain discovery confirmed using:


realm discover sbxqiao.lab


Domain join executed:


realm join sbxqiao.lab


Join result:


configured: kerberos-member


The computer object appeared in Active Directory.

---

# Identity Resolution Test

Active Directory identities confirmed using:


id administrator@sbxqiao.lab


Result:

Linux correctly resolves AD users and group membership via SSSD.

---

# Server Placement

The Linux server object was moved to the correct OU:


SBX-T1 → Servers


This aligns the server with Tier-1 administrative policy scope.

---

# Tier Model Enforcement

OU inheritance blocked to enforce policy isolation.


SBX-T0 → Block Inheritance
SBX-T1 → Block Inheritance
SBX-T2 → Block Inheritance


This prevents domain GPOs from leaking across tiers.

---

# Result

The lab now supports a hybrid identity environment:


Windows Servers → controlled by GPO
Linux Servers → controlled by SSSD
Active Directory → central identity provider


Linux authentication is now fully integrated with the enterprise identity system.

---

# Current Architecture State


Tier 0
Domain Controllers

Tier 1
Servers
Linux Infrastructure

Tier 2
Workstations


Authentication flow:


Linux login
↓
PAM
↓
SSSD
↓
Kerberos
↓
Active Directory


---

# Next Planned Steps

1. Implement SSSD access control for Tier-1 servers
2. Configure AD group based sudo privileges
3. Implement Linux file sharing using Samba with AD authentication
4. Introduce privileged access workstations (PAW)
5. Automate Linux domain join using Ansible