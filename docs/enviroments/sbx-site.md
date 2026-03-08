# SBX Site

Primary infrastructure site.

Location:
Host A (Main Hyper-V workstation)

Subnet:
172.16.50.0/24

Gateway:
172.16.50.1

Components:

- SBX-RTR1 (pfSense firewall)
- SBX-DC1 (Active Directory / DNS)
- SBX-CL1 (Windows workstation)
- SBX-LX1 (Linux server)

Purpose:

SBX represents the primary enterprise site where the identity infrastructure is hosted.