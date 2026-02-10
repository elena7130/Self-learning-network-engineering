**Date:** 2026-02-10

**Topology:** 

<img width="1904" height="700" alt="image" src="https://github.com/user-attachments/assets/eafb619d-caf0-47b6-9433-d5884bdec036" />


## Goal

The routers in the network aren't receiving the routes they should from OSPF.

R5 isn't receiving the 10.0.0.0/8 summary route it should.
Troubleshoot and fix the issues.  

Not all routers are misconfigured.
  
## R4: Troubleshooting & Resolution

Initial Check: I ran show ip route ospf and found that the routing table on R4 was empty.

Interface Verification: I checked the IP addresses using show ip interface brief; all addresses were configured correctly.

Protocol Analysis: Using show ip protocols, I checked the advertised networks and passive interfaces. I discovered that interface g0/0 was configured as a passive interface. This prevented R4 from forming OSPF adjacencies or receiving routes on that segment.

Configuration Fix:

Bash
router ospf 1
 no passive-interface g0/0
Verification: After the fix, I verified the routing table with show ip route ospf. The routes for 10.14.0.0 and 2.2.2.2 appeared, and R1 successfully became an OSPF neighbor with R4.

R1: Verification
Checked the routing table and protocol status using show ip route and show ip protocols.

Confirmed that R1 has successfully established OSPF neighbor relationships with both R4 and R2.

R2: Troubleshooting & Resolution
Neighbor Status: Only R1 was showing as a neighbor. I suspected an issue on the link between R2 and R3.

Interface Status: show ip interface brief revealed that interface f2/0 on R2 was administratively down.

Configuration Fix:

Bash
interface f2/0
 no shutdown
Network Validation: I confirmed the network advertisements are correct: 10.2.0.0 is in Area 1 and 10.23.0.0 is in Area 0.

R3: Troubleshooting & Resolution
Area Mismatch: I discovered that the network 10.23.0.0 was assigned to the wrong area.

Configuration Fix:

Bash
router ospf 1
 no network 10.23.0.0 [wildcard_mask] area [wrong_area]
 network 10.23.0.0 [wildcard_mask] area 0
Verification: After correcting the area, R2 and R5 successfully formed neighbor adjacencies with R3.
