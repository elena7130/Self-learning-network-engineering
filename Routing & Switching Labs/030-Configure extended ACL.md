**Date:** 2026-02-09

**Topology:** 
<img width="1535" height="685" alt="image" src="https://github.com/user-attachments/assets/1cc865a2-67f5-4ae4-ad32-b8b638b0c3bc" />




## Goal

Configure extended ACLs to achieve the following requirements:
    only PC1 can access SRV1
    only hosts on the 192.168.2.0/24 network can access SRV2

  
## Configuration - only PC1 can access SRV1 and only hosts on the 192.168.2.0/24 network can access SRV2

```
R2(config)ip access-list extended 101
R2(config-std-nacl)permit ip host 192.168.2.14 host 192.168.3.100
R2(config-std-nacl)deny ip any host host 192.168.3.100
R2(config-std-nacl)permit ip 192.168.2.0 0.0.0.255 host 192.168.3，101
R2(config-std-nacl)deny ip any host 192.168.3.101
R2(config-std-nacl)permit ip any any
R2(config)interface f0/0
R2(config-if)ip access-group 101 out 
```

