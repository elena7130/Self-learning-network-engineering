**Date:** 2026-02-11

**Topology:**
<img width="1298" height="438" alt="image" src="https://github.com/user-attachments/assets/c0cf78cd-7997-4938-9810-451929236c83" />


## Goal：

1. RIP has been configured so that R1 and R2 can reach their inside networks. Why can't PC1, PC2, and PC3 successfully ping SRV1?
    (Hint: The serial connection between R1 and R2 is simulating the Internet with ACLs)
    
2. Configure static NAT on R1 to translate the address of PC1, PC2, and PC3 to1.2.3.11, 1.2.3.12, and 1.2.3.13, respectively.

3. Attempt to ping SRV1 from each PC again. Do the pings succeed?

## Answer 1

- PC1, PC2, and PC3 cannot ping SRV1 , because PCs' IP addresses are private addresses , so they can't be routed over the Internet . 
## Configuration - R1

```
R1(config)ineterface g0/0
R1(config-if)ip nat inside
R1(config)ineterface s0/3/0
R1(config-if)ip nat outside
R1(config)ip route inside source 192.168.1.11 1.2.3.11
R1(config)ip route inside source 192.168.1.12 1.2.3.12
R1(config)ip route inside source 192.168.1.13 1.2.3.13
```
