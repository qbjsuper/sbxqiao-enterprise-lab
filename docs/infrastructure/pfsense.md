# pfSense Firewall Deployment

This document describes the pfSense firewall deployment used in the SBXQIAO Enterprise Lab.

---

## Purpose

pfSense virtual appliances act as the network gateways for each simulated site.

Responsibilities include:

- Routing
- NAT
- Firewall filtering
- DHCP services
- VPN connectivity

---

## Firewall Instances

Two firewall instances are planned.

| System | Role |
|------|------|
| pfSense-A | Gateway for SBX site |
| pfSense-B | Gateway for SBY site |

---

## Interface Layout

Each firewall uses two network interfaces.

| Interface | Network | Purpose |
|---------|--------|--------|
| WAN | vSwitch-WAN | Internet connectivity |
| LAN | vSwitch-SBX / vSwitch-SBY | Site internal network |

---

## SBX Firewall

Interfaces:

| Interface | Network |
|------|------|
| WAN | vSwitch-WAN |
| LAN | vSwitch-SBX |

LAN configuration:

| Setting | Value |
|------|------|
| IP Address | 172.16.50.1 |
| Subnet | 255.255.255.0 |

This interface acts as the default gateway for the SBX network.

---

## SBY Firewall

Interfaces:

| Interface | Network |
|------|------|
| WAN | vSwitch-WAN |
| LAN | vSwitch-SBY |

LAN configuration:

| Setting | Value |
|------|------|
| IP Address | 172.16.60.1 |
| Subnet | 255.255.255.0 |

---

## Planned Services

pfSense will eventually provide:

- DHCP services for lab networks
- DNS forwarding
- Site-to-site VPN
- Firewall rule management

---

## Site-to-Site VPN Plan

The two firewalls will be connected using:

`IPsec VPN`

Connection:

```text
pfSense-A ⇄ IPsec ⇄ pfSense-B
This will allow communication between:

SBX site

SBY site

Future Experiments

The firewall environment will allow testing of:

NAT behavior

firewall rule design

VPN troubleshooting

routing behavior

network segmentation