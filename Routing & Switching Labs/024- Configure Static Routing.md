**Date:** 2026-02-2

**Topology:** 

<img width="1413" height="217" alt="image" src="https://github.com/user-attachments/assets/8cbea412-ad26-427b-bb6e-370832b6369f" />


## Goal
1. Configure the G0/0 and G0/1 interfaces of R1 and R2 according to the network diagram, and enable the interfaces.

2. Configure static routes on R1 and R2 to allow PC1 to reach PC2, and vice versa.
    Configure the routes to the subnets the PCs are part of, not directly to the PCs.
    Test by using ping or tracert from each PC.

  
## Configuration - interface IP address

```
R1(config)interface g0/1
R1(config-if)ip address 192.168.1.1 255.255.255.0
R1(config-if)no shutdown
R1(config-if)interface g0/0
R1(config-if)ip address 10.0.0.1 255.255.255.0
R1(config-if)no shutdown
```

```
R2(config)interface g0/1
R2(config-if)ip address 192.168.2.1 255.255.255.0
R2(config-if)no shutdown
R2(config-if)interface g0/0
R2(config-if)ip address 10.0.0.2 255.255.255.0
R2(config-if)no shutdown
```

## Configuration - static routes

```
R1(config)ip route 192.168.2.0 255.255.255.0 10.0.0.2
R1(config)do sh ip route

* When I see **'S 192.168.2.0/24 [1/0] via 10.0.0.2'** in the routing table, it means the static route was configured successfully.
```

```
R2(config)ip route 192.168.1.0 255.255.255.0 10.0.0.1
R1(config)do sh ip route
```

## Configuration - checking on PC 1 

```
tracert 192.168.2.12
```
