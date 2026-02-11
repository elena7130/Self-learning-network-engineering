**Date:** 2026-02-11

**Topology:**
<img width="1470" height="482" alt="image" src="https://github.com/user-attachments/assets/113d5494-626c-43ad-b185-d76a48f88364" />


## Goal：

1. Configure dynamic NAT on R1 to translate the 192.168.1.0/24 subnet to the address range 1.2.3.10 - 1.2.3.20

2. Ping from each PC to SRV1, then use a show command on R1 to check the translations.

## Configuration - R1

```
R1(config)ineterface g0/0
R1(config-if)ip nat inside
R1(config)ineterface s0/3/0
R1(config-if)ip nat outside
R1(config)access-list 1 permit 192.168.1.0 0.0.0.255
R1(config)ip route pool 1POOL 1.2.3.10 1.2.3.20 netmask 255.255.255.0
R1(config)ip route inside source lis 1 pool 1POOL 
```
