# Lab 05: Secure Corporate Network (VLAN + Inter-VLAN Routing + ACL + Port Security)

## Goal

Segment a corporate LAN into Sales (VLAN 10) and IT (VLAN 20), enable inter-VLAN routing with Router-on-a-Stick, restrict traffic with an extended ACL, and protect an access port with port security.

## Topology

- **HQ-Router** (Router-on-a-Stick): Gig0/0.10 (192.168.10.1/24) and Gig0/0.20 (192.168.20.1/24)
- **Access-Switch**: Fa0/1 (VLAN 10, Sales-PC), Fa0/2 and Fa0/3 (VLAN 20, IT-PC-1 and IT-PC-2), Gi0/1 trunk to router
- **Sales-PC**: 192.168.10.2/24, gateway 192.168.10.1
- **IT-PC-1**: 192.168.20.2/24, gateway 192.168.20.1
- **IT-PC-2**: 192.168.20.3/24, gateway 192.168.20.1

## Configuration Summary

- VLAN 10 named Sales, VLAN 20 named IT
- Trunk on switch uplink to router (Router-on-a-Stick, 802.1Q)
- Extended ACL 100 on HQ-Router: deny 192.168.10.2 to 192.168.20.2, permit all other IP traffic
- Port security on Fa0/1: maximum 1 MAC, sticky MAC, violation mode shutdown

## Verification

**VLAN (Access-Switch):** `show vlan brief` shows VLAN 10 (Sales) on Fa0/1 and VLAN 20 (IT) on Fa0/2, Fa0/3.

**Port security (Access-Switch):** `show port-security interface fa0/1` shows Enabled, Secure-up, Maximum MAC 1, Sticky MAC 1, Violation Mode Shutdown.

**ACL (HQ-Router):** `show access-lists` shows deny line for 192.168.10.2 to 192.168.20.2 and permit ip any any.

**Inter-VLAN routing:** Sales-PC to IT-PC-2 (192.168.20.3) ping succeeds (3 of 4 replies).

**ACL test:** Sales-PC to IT-PC-1 (192.168.20.2) ping is blocked. Reply is `Destination host unreachable` from 192.168.10.1, which confirms the ACL drop.
**Trunk (Access-Switch):** `show interfaces trunk` shows Gig0/1 in `802.1q trunking` mode, allowed and active VLANs 1, 10, 20, which confirms the Router-on-a-Stick uplink.

## File

- `Secure_Corporate_Network.pkt`
