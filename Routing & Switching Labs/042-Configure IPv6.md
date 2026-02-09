**Date:** 2026-02-09

**Topology:** 

<img width="1439" height="781" alt="image" src="https://github.com/user-attachments/assets/cf394a63-b439-4047-b320-0c1adb2ec58c" />



## Goal

1. Enable IPv6 on R1, R2, and R3, and configure the IPv6 addresses on:
    R1's G0/0 and G0/1 interfaces
    R2's G0/1 interface
    R3's G0/1 interface
2. Configure SLAAC on R2 and R3's G0/0 interfaces
3. Configure static IPv6 routes to provide full connectivity to the network

  
## Configuration - on R1 /R2/ R3

```
R1(config)interface g0/1
R1(config-if)ipv6 address 2001:db8:1:1::1/64
R1(config-if)no shutdown
R1(config-if)interface g0/0
R1(config-if)ipv6 enbale
```

```
R2(config)interface g0/1
R2(config-if)ipv6 address 2001:db8:2:2::1/64
R2(config-if)no shutdown
R2(config-if)interface g0/0
R2(config-if)ipv6 enbale
```

```
R3(config)interface g0/1
R3(config-if)ipv6 address 2001:db8:3:3::1/64
R3(config-if)no shutdown
R3(config-if)interface g0/0
R3(config-if)ipv6 enbale
```

## Configuration-SLAAC on R2 and R3

```
R2(config)interface g0/0
R2(config-if)ipv6 address autoconfig
```

```
R3(config)interface g0/0
R3(config-if)ipv6 address autoconfig
```

## Configuration-IPv6 routes


G0/0 link local addresses on R1 :FE80::20C:CFFF:FE58:C801
G0/0 link local addresses on R2 :FE80::2D0:FFFF:FE69:3801
G0/0 link local addresses on R3 :FE80::2E0:8FFF:FE8A:7101

```
R1(config)ip route 2001:db8:2:2::/64 g0/0 FE80::2D0:FFFF:FE69:3801
R1(config)ip route 2001:db8:3:3::/64 g0/0 FE80::2E0:8FFF:FE8A:7101
R1(config)ipv6 unicast-routing
```

```
R2(config)ip route 2001:db8:1:1::/64 g0/0 FE80::20C:CFFF:FE58:C801
R2(config)ip route 2001:db8:3:3::/64 g0/0 FE80::2E0:8FFF:FE8A:7101
R2(config)ipv6 unicast-routing
```

```
R3(config)ip route 2001:db8:1:1::/64 g0/0 FE80::20C:CFFF:FE58:C801
R3(config)ip route 2001:db8:2:2::/64 g0/0 FE80::2D0:FFFF:FE69:3801
R3(config)ipv6 unicast-routing
```
