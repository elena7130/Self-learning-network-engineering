**Date:** 2026-02-09

**Topology:** 

<img width="1507" height="683" alt="image" src="https://github.com/user-attachments/assets/a236e042-1f3e-4a76-9447-42039d4cded6" />



## Goal

Configure standard ACLs to achieve the following requirements:
    only computers in the 192.168.1.0/24 network can access SRV1
    PC4 cannot communicate with the 192.168.1.0/24 network.

  
## Configuration - only computers in the 192.168.1.0/24 network can access SRV1

```
R2(config)ip access-list standard 1
R2(config-std-nacl)permit 192.168.1.0 0.0.0.255
R2(config)interface f0/0
R2(config-if)ip access-group 1 out
```


## Configuration - PC4 cannot communicate with the 192.168.1.0/24 network

```
R1(config)ip access-list standard 1
R2(config-std-nacl)permit host 192.168.1.14 
R2(config-std-nacl)permit any
R2(config-std-nacl)interface f0/0
R2(config-if)ip access-group 1 out
```
