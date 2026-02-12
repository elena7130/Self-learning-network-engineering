**Date:** 2026-02-02

## Requirement:

The following figure shows three routers and their IP addresses. The routers all use an initial configuration that matches the three examples listed here as well. Your job is to add static routes to the LAN subnets, per the following specific instructions:

1. Routers R1 and R2 should use static routes whose configuration refers to an IP address in the command.
2. Router R3 should use static routes that refer to the outgoing interface in the command.
3. If your configuration was implemented, all three routers should have a connected route to their own LAN subnet, and a static route to each of the other two LAN subnets.
4. Do not add static routes for the WAN subnets

**Topology:** 
<img width="594" height="586" alt="image" src="https://github.com/user-attachments/assets/3ddacd0d-8306-49c9-8ce3-1cf2332c3fba" />



## Configuration on R1

``` 
R1(config)ip route 172.16.2.0 255.255.254.0 10.1.1.130
# R1 to R2 
R1(config)ip route 10.1.89.0 255.255.255.128 10.1.88.130
# R1 to R3
```

## Configuration on R2
```
R2(config)ip route 10.1.89.0 255.255.255.128 172.16.0.2 
# R2 to R3 
R2(config)ip route 10.1.87.0 255.255.255.128 10.1.1.129 
# R2 to R1
```

## Configuration on R3
```
R3(config)ip route 172.16.2.0 255.255.254.0 10.1.88.129
# R3 to R2 
R3(config)ip route 10.1.89.0 255.255.255.128 172.16.0.1
# R3 to R1
```
*Lab Resource* :https://www.certskills.com/clab206/
