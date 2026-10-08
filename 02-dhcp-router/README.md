# DHCP Server on Cisco Router

## Overview

This lab demonstrates how to configure a Cisco router as a DHCP server for multiple VLANs using Router-on-a-Stick for inter-VLAN routing.

## Objectives

* Create VLAN 10 (USERS) and VLAN 20 (ADMIN)
* Configure access ports on the switch
* Configure a trunk link between the switch and router
* Configure Router-on-a-Stick
* Configure the Cisco router as a DHCP server
* Automatically assign IP addresses to PCs
* Configure default gateways and DNS
* Verify DHCP and inter-VLAN connectivity

## Topology

```text
PC0 ──┐
      ├── Switch 2960 ─── Router 2911
PC1 ──┘
```

## VLAN & IP Addressing

| Device | VLAN | IP Address            | Gateway        |
| ------ | ---: | --------------------- | -------------- |
| PC0    |   10 | DHCP (`192.168.10.x`) | `192.168.10.1` |
| PC1    |   20 | DHCP (`192.168.20.x`) | `192.168.20.1` |

### VLANs

| VLAN | Name  | Network           |
| ---: | ----- | ----------------- |
|   10 | USERS | `192.168.10.0/24` |
|   20 | ADMIN | `192.168.20.0/24` |

## Switch Configuration

* `Fa0/1` → PC0 → Access VLAN 10
* `Fa0/2` → PC1 → Access VLAN 20
* `Fa0/3` → Router → Trunk

## Router Configuration

### Router-on-a-Stick

* `G0/0.10` → VLAN 10 → `192.168.10.1/24`
* `G0/0.20` → VLAN 20 → `192.168.20.1/24`

### DHCP

The router provides DHCP services for both VLANs.

* VLAN 10 DHCP pool → `192.168.10.0/24`
* VLAN 20 DHCP pool → `192.168.20.0/24`
* Default gateways:

  * VLAN 102-dhcp-router0 → `192.168.10.1`
  * VLAN 20 → `192.168.20.1`
* DNS Server → `8.8.8.8`

## Verification

### PC0

PC0 successfully received:

```text
IP Address:      192.168.10.2
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.10.1
```

### PC1

PC1 successfully received:

```text
IP Address:      192.168.20.2
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.20.1
```

### Connectivity Tests

* PC0 → VLAN 10 Gateway: Successful
* PC1 → VLAN 20 Gateway: Successful
* PC1 → PC0 (`192.168.10.2`): Successful
* Inter-VLAN communication: Successful

### DHCP Verification

The router showed active DHCP leases using:

```text
show ip dhcp binding
```

Example:

```text
192.168.10.2
```

## Skills Practiced

* VLAN configuration
* Access ports
* Trunking
* 802.1Q
* Router-on-a-Stick
* DHCP configuration
* IP addressing
* Default gateways
* Inter-VLAN routing
* Network troubleshooting
* Cisco IOS CLI

## Tools

* Cisco Packet Tracer
* Cisco 2911 Router
* Cisco 2960 Switch

## Outcome

Successfully configured and verified a multi-VLAN network where a Cisco router provides DHCP services and enables communication between VLAN 10 and VLAN 20.
