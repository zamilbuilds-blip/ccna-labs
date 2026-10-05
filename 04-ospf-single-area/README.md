# Lab 04: Multi-Branch OSPF Single Area

## Goal

Configure OSPFv2 (Process 1, Area 0) across three routers so that all LAN subnets are reachable from each other through dynamic routing.

## Topology

- **R1-HQ** connected to R2-Branch-A and R3-Branch-B (WAN links)
- **R2-Branch-A** connected to R3-Branch-B (WAN link)
- Each router has a LAN:
  - HQ LAN: 192.168.10.0/24 (HQ-PC)
  - Branch-A LAN: 192.168.20.0/24 (Branch-A-PC)
  - Branch-B LAN: 192.168.30.0/24 (Branch-B-PC)

## Technologies

- OSPFv2 (Process ID 1, Area 0)
- Point-to-point WAN links
- Static IP addressing

## Verification

- `show ip ospf neighbor` (neighbors should show FULL)
- `show ip route ospf` (OSPF routes present)
- Ping from Branch-B-PC (192.168.30.x) to HQ-PC (192.168.10.x)

## File

- `OSPF_Single_Area_Network.pkt`
