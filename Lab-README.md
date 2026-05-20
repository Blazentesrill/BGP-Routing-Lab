# Lab 3: Exploring EIGRP, OSPF, and BGP

## Overview
Configured and analyzed intra-domain and inter-domain routing protocols across a three-AS network in Cisco Packet Tracer. Then simulated two real-world BGP vulnerabilities: route flapping and route hijacking.

## Tools Used
- Cisco Packet Tracer
- Cisco ISR4331 Routers
- Cisco 2960-24TT Switches

## Network Topology
```
        AS100 (EIGRP)           AS200 (BGP only)
    R0 ── R1 ── R2 ──── R3
                 |              |
                BGP            BGP
                 |              |
                R6 ──── R4 ── R5
        AS300 (OSPF)
```
- Intra-AS links: `10.z.xy.0/24`
- Inter-AS links: `200.z.xy.0/30`
- *(z derived from student ID)*

## What I Did

### Task 1: Protocol Configuration
- **EIGRP (AS100):** Configured Router 1 to participate in EIGRP alongside pre-configured Routers 0 and 2; advertised internal networks using wildcard masks
- **OSPF (AS300):** Configured Router 5 for single-area OSPF alongside pre-configured Routers 4 and 6
- **BGP:** Configured Router 2 to peer with R3 (AS200) and R6 (AS300) via eBGP, and redistributed EIGRP routes into BGP so internal AS100 prefixes propagate to other ASes
- Timed route convergence after each router was added and observed how routing tables in R2, R3, and R6 updated
- Verified final forwarding tables showing routes tagged with EIGRP (D), OSPF (O), and BGP (B) origin codes

### Task 2: Route Flapping
- Alternated the R0–Switch1 and R4–Switch2 interfaces up/down to cause prefix withdrawals and re-advertisements
- Observed BGP UPDATE messages in simulation mode showing repeated route changes before stabilization
- Documented how flapping in one AS propagates instability across all three ASes via BGP

### Task 3: Route Hijacking
- Enabled both Switch1 and Switch2 interfaces simultaneously to create a scenario where two ASes advertise overlapping prefixes
- Observed BGP speakers selecting incorrect or conflicting best paths
- Analyzed UPDATE packet payloads to understand how hijacking manifests in routing tables

## Key Concepts Demonstrated
- EIGRP wildcard mask network advertisement
- OSPF single-area configuration and DR/BDR election
- eBGP peering, AS-path attributes, and route redistribution
- BGP convergence timing vs. IGP convergence timing
- Route flapping mechanics and its effect on network stability
- BGP route hijacking via prefix advertisement conflicts

## Files
- `lab3.pkt` — Packet Tracer file with all routers fully configured for Task 1
