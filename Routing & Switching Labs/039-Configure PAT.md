**Date:** 2026-02-11

**Topology:**
![Uploading image.png…]()



## Goal：

1. Configure PAT on R1 to translate addresses in the 192.168.1.0/24 network to R1's S0/3/0 interface.(make sure to 'overload' the interface!)

2. Ping from each PC to SRV1, then use a show command on R1 to check the translations.

## Configuration - R1

```
R1(config)ineterface g0/0
R1(config-if)ip nat inside
R1(config)ineterface s0/3/0
R1(config-if)ip nat outside
R1(config)access-list 1 permit 192.168.1.0 0.0.0.255
R1(config)ip route inside source lis 1 interface s0/3/0 overload 
```
