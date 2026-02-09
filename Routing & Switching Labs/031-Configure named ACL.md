**Date:** 2026-02-09

**Topology:** 
<img width="1427" height="654" alt="image" src="https://github.com/user-attachments/assets/b9c37c52-0ff1-464a-9aaa-c844cc4ba833" />





## Goal

Configure named standard ACLs to achieve the following requirements:
    Hosts in the 192.168.1.0/24 and 192.168.2.0/24 networks cannot communicate with eachother
    Hosts in the 192.168.2.0/24 network cannot access the 192.168.3.0/24 network

  
## Configuration - Hosts in the 192.168.1.0/24 and 192.168.2.0/24 networks cannot communicate with eachother

```
R1(config)ip access-list standard deny1
R1(config-std-nacl)deny ip 192.168.1.0 0.0.0.255
R1(config-std-nacl)permit any
R1(config)ip access-list standard deny2
R1(config-std-nacl)deny ip 192.168.2.0 0.0.0.255
R1(config-std-nacl)permit any
R1(config)interface f0/0
R1(config-if)ip access-group deny2 out 
R1(config)interface f1/0
R1(config-if)ip access-group deny1 out 
```

## Configuration - Hosts in the 192.168.2.0/24 network cannot access the 192.168.3.0/24 network

```
R2(config)ip access-list standard deny2
R2(config-std-nacl)deny ip 192.168.2.0 0.0.0.255
R21(config-std-nacl)permit any
R2(config)interface f0/0
R1(config-if)ip access-group deny2 out 
```
