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

**OSPF neighbors (R1-HQ):**
Both neighbors (192.168.20.1 and 192.168.30.1) reach the `FULL/DR` state on Gi0/0 and Gi0/1.

**OSPF routes learned (R1-HQ):**
- 192.168.20.0/24 via 10.1.12.2 (Gi0/0)
- 192.168.30.0/24 via 10.1.20.1 (Gi0/1)
- 10.1.13.0/24 via two equal-cost paths

**End-to-end ping (Branch-B-PC to HQ-PC, 192.168.10.2):**
3 of 4 packets received (first packet timed out while ARP resolved; remaining replies TTL=126, <1ms).

## File

- `OSPF_Single_Area_Network.pkt`
