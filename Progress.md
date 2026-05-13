# PROJECT STATUS — MIU Network Project

## Topology Overview
- **4 Buildings:** Main, S, N, R — each has 1 MLS + 2 access switches (SW1, SW2)
- **Branch:** Branch-GW router + 2 access switches (B_S1, B_S2)
- **Servers:** DHCP, DNS, Web, Email, NTP connected to SW-S (L3 switch), which connects to MIU-GW
- **MIU-GW** connects to ISP, all 4 MLSs, and SW-S

---

## Addressing Table

| Device | Interface | IP | Subnet | Gateway | VLAN |
|--------|-----------|-----|--------|---------|------|
| Main-MLS | G1/1/1 | 10.0.1.33 | 255.255.255.252 | N/A | N/A |
| Main-MLS | VLAN 110 | 10.0.0.161 | 255.255.255.224 | 10.0.1.34 | 110 |
| Main-MLS | VLAN 120 | 10.0.0.65 | 255.255.255.192 | 10.0.1.34 | 120 |
| S-MLS | G1/1/1 | 10.0.1.41 | 255.255.255.252 | N/A | N/A |
| S-MLS | VLAN 25 | 10.0.0.225 | 255.255.255.240 | 10.0.1.42 | 25 |
| S-MLS | VLAN 140 | 10.0.0.1 | 255.255.255.192 | 10.0.1.42 | 140 |
| N-MLS | G1/1/1 | 10.0.1.37 | 255.255.255.252 | N/A | N/A |
| N-MLS | VLAN 150 | 10.0.0.129 | 255.255.255.224 | 10.0.1.38 | 150 |
| N-MLS | VLAN 160 | 10.0.0.241 | 255.255.255.240 | 10.0.1.38 | 160 |
| R-MLS | G1/0/5 | 10.0.1.45 | 255.255.255.252 | N/A | N/A |
| R-MLS | VLAN 170 | 10.0.0.193 | 255.255.255.224 | 10.0.1.46 | 170 |
| R-MLS | VLAN 180 | 10.0.1.1 | 255.255.255.240 | 10.0.1.46 | 180 |
| MIU-GW | Gig0/0 | 209.165.200.226 | 255.255.255.240 | N/A | N/A |
| MIU-GW | Gig0/1 | 10.0.1.46 | 255.255.255.252 | N/A | N/A |
| MIU-GW | Gig0/0/0 | 10.0.1.17 | 255.255.255.240 | N/A | N/A |
| MIU-GW | Gig0/1/0 | 10.0.1.34 | 255.255.255.252 | N/A | N/A |
| MIU-GW | Gig0/2/0 | 10.0.1.42 | 255.255.255.252 | N/A | N/A |
| MIU-GW | Gig0/3/0 | 10.0.1.38 | 255.255.255.252 | N/A | N/A |
| ISP | Gig0/0 | 209.165.200.225 | 255.255.255.240 | N/A | N/A |
| ISP | Gig0/1 | 64.100.1.1 | 255.255.255.224 | N/A | N/A |
| ISP | Gig0/2 | 64.100.2.1 | 255.255.255.224 | N/A | N/A |
| Branch-GW | G0/0.2 | 192.168.2.1 | 255.255.255.0 | N/A | 2 |
| Branch-GW | G0/0.3 | 192.168.3.1 | 255.255.255.0 | N/A | 3 |
| Branch-GW | G0/1 | 64.100.1.2 | 255.255.255.224 | N/A | N/A |
| SW-S | G1/1/1 (L2 access) | N/A | N/A | N/A | 10 |
| SW-S | VLAN 10 (SVI) | 10.0.1.18 | 255.255.255.240 | 10.0.1.17 | 10 |

---

## Server IPs (SW-S, VLAN 10, subnet 10.0.1.16/28)

| Server | IP | Gateway |
|--------|-----|---------|
| DHCP | 10.0.1.19 | 10.0.1.18 |
| DNS | 10.0.1.20 | 10.0.1.18 |
| Web | 10.0.1.21 | 10.0.1.18 |
| Email | 10.0.1.22 | 10.0.1.18 |
| NTP | 10.0.1.23 | 10.0.1.18 |

---

## PC IP Assignments

| Building | VLAN | Subnet | Gateway | PCs |
|----------|------|--------|---------|-----|
| Main | 110 | 10.0.0.160/27 | 10.0.0.161 | PC1, PC2 |
| Main | 120 | 10.0.0.64/26 | 10.0.0.65 | PC3, PC4 |
| S | 25 | 10.0.0.224/28 | 10.0.0.225 | PC5, PC6 |
| S | 140 | 10.0.0.0/26 | 10.0.0.1 | PC7, PC8 |
| N | 150 | 10.0.0.128/27 | 10.0.0.129 | PC9, PC10 |
| N | 160 | 10.0.0.240/28 | 10.0.0.241 | PC11, PC12 |
| R | 170 | 10.0.0.192/27 | 10.0.0.193 | PC13, PC14 |
| R | 180 | 10.0.1.0/28 | 10.0.1.1 | PC15, PC16 |
| Branch | 2 | 192.168.2.0/24 | 192.168.2.1 | PC-11 |
| Branch | 3 | 192.168.3.0/24 | 192.168.3.1 | PC-12 |

---

## ✅ COMPLETED

- Basic config (hostname, no ip domain-lookup, service password-encryption, MOTD, SSH)
- All IP addressing on all devices
- VLANs + Access ports for all buildings
- EtherChannels (LACP) between MLS access switches and access switches each other
- Static routing (default routes on all MLS MIU-GW, routes on MIU-GW all buildings)
- Part 4 Routing Protocols: OSPF (100) on MIU-GW/Main-MLS/S-MLS, EIGRP (AS 10) on MIU-GW/N-MLS/R-MLS, Redistribution on MIU-GW
- Part 5 DHCP: Pools on Main-MLS (VLAN110,120,25,140), Branch-GW (B-LAN2, B-LAN3), all PCs getting IPs, IP helpers configured

---

## 🔴 REMAINING

- Part 6 — NAT (Dynamic PAT + Static NAT) — done except final verification (Step 5 ping tests need troubleshooting)
- Part 7 — Network Management (NTP, Syslog, DNS, Email, Web)
- Part 8 — Site-to-Site IPsec VPN (MIU-GW Branch-GW)
- Part 9 — Wireless Home Router
- Part 10 — Verify Connectivity (screenshots)
- Part 11 — Documentation

---

## Key Commands Used

- Each MLS: `ip routing`, default routes, SVIs with `ip helper-address`
- Branch-GW: `ip routing`, subinterfaces dot1q, DHCP pools
- SW-S: VLAN 10, access ports for servers, SVI 10.0.1.18/28, default route 10.0.1.17
- All trunks set to **native VLAN 10**
- OSPF process 100 on MIU-GW + Main-MLS + S-MLS
- EIGRP AS 10 on MIU-GW + N-MLS + R-MLS
- Redistribution on MIU-GW
