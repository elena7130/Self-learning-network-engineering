**Date:** 2026-02-10

**Topology:** 

<img width="1904" height="700" alt="image" src="https://github.com/user-attachments/assets/eafb619d-caf0-47b6-9433-d5884bdec036" />


## Goal

The routers in the network aren't receiving the routes they should from OSPF.

R5 isn't receiving the 10.0.0.0/8 summary route it should.
Troubleshoot and fix the issues.  

Not all routers are misconfigured.
  
## Configuration - checking on R4

1. Through`show ip route ospf ` , I find that no route table in R4
2. Then I find that whether ip address is correct through `show ip interface brief` , they are correct . 
3. Through `show ip protocal`and check networks , passive interface , I found that g0/0 is in the passive interface , which possibility cause issue that no ospf route on R4 
4. Configure :
     route ospf 1
     no passive-interface g0/0
5.  check `show ip route ospf `, then it works and I find the network 10.14.0.0 and 2.2.2.2 in the table and R1 is the ospf neighbour with R4


## Configuration - checking on R1

  1. Checking on R1 with command `show ip route ` ,`show ip protocal`. 
  2. R4 and R2 are OSPF neighbour with R1
  
## Configuration - checking on R2 

1. Only R1 is the neighour with R2 , so there are probably some issues between with R2 and R4  
2. Through `show ip interface breif`, I find that interface f2/0 on R2 is down , so configure `no shutdown`on that interface
3. The networks on R2 are correct . That means , 10.2.0.0 in area 1 and 10.23.0.0 in area 0 

## Configuration - checking on R3

1. I find that network 10.23.0.0 is in the wrong area . 
2. configure `route ospf 1 10.23.0.0 area 0 `
3. Then R2 and R5 are neighbours with R3


If R5 could ping R4 , that means the lab is success .
