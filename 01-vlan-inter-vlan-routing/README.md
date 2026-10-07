# VLAN & Inter-VLAN Routing Lab

## Overview

A hands-on Cisco networking lab built using Cisco Packet Tracer to practice VLAN segmentation and inter-VLAN communication using Router-on-a-Stick.

## Objectives

* Create and configure multiple VLANs.
* Assign switch ports to VLANs.
* Configure an 802.1Q trunk link.
* Configure router subinterfaces.
* Implement inter-VLAN routing.
* Configure IPv4 addressing and default gateways.
* Verify connectivity and troubleshoot network communication.

## Network Topology

**Devices:**

* 1 × Cisco 2911 Router
* 1 × Cisco Switch
* 2 × PCs

**VLANs:**

| VLAN | Name  | Network         | Gateway      |
| ---- | ----- | --------------- | ------------ |
| 10   | USERS | 192.168.10.0/24 | 192.168.10.1 |
| 20   | ADMIN | 192.168.20.0/24 | 192.168.20.1 |

**IP Addressing:**

| Device | IP Address       | VLAN    |
| ------ | ---------------- | ------- |
| PC0    | 192.168.10.10/24 | VLAN 10 |
| PC1    | 192.168.20.20/24 | VLAN 20 |

## Configuration

### VLAN Configuration

Configured VLAN 10 and VLAN 20 on the switch and assigned the corresponding access ports.

### Trunk Configuration

Configured the switch port connected to the router as an 802.1Q trunk.

### Router-on-a-Stick

Configured router subinterfaces:

* G0/0.10 → 192.168.10.1/24
* G0/0.20 → 192.168.20.1/24

Each subinterface was associated with its corresponding VLAN using 802.1Q encapsulation.

## Verification

Connectivity was tested between each PC and its default gateway.

Inter-VLAN connectivity was then verified by successfully pinging:

`192.168.10.10 → 192.168.20.20`

The successful ping confirmed that the router was correctly routing traffic between VLAN 10 and VLAN 20.

## Troubleshooting

During the lab, the router subinterface addressing was verified using:

`show ip interface brief`

An incorrect/unassigned IP address on the VLAN 10 subinterface was identified and corrected.

This restored connectivity between the VLAN 10 host and its gateway.

## Skills Practiced

* VLAN configuration
* Access ports
* 802.1Q trunking
* Router-on-a-Stick
* Inter-VLAN routing
* IPv4 addressing
* Default gateways
* Cisco IOS CLI
* Network troubleshooting
* Connectivity verification

## Tools

* Cisco Packet Tracer
* Cisco IOS CLI

## Outcome

Successfully implemented and tested communication between two separate VLANs using Router-on-a-Stick.


