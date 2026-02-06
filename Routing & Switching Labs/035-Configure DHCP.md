**Date:** 2026-02-06

**Topology:** 
<img width="1460" height="555" alt="image" src="https://github.com/user-attachments/assets/ac263513-588e-45f4-ac49-b90fea06d4c8" />



## Goal

1. Configure three DHCP pools on R1:
    10pool:
    Range: 10.0.0.0/24
    Default gateway: 10.0.0.1
    DNS server: 10.0.0.1
    Excluded addresses: 10.0.0.1 - 10.0.0.10


    20pool:
    Range: 20.0.0.0/24
    Default gateway: 20.0.0.1
    DNS server: 20.0.0.1
    Excluded addresses: 20.0.0.1 - 20.0.0.10


    12pool:
    Range: 192.168.12.0/24

2. Configure R2's G0/0 interface as a DHCP client, then enable the interface
3. Configure R2's G0/1 interface as a DHCP relay agent so that hosts on the 20.0.0.0/24 network can get IP addresses

  
## Configuration - set DHCP server on R1

```
ip dhcp excluded-address 10.0.0.1 10.0.0.10
ip dhcp excluded-address 20.0.0.1 20.0.0.10
ip dhcp pool 10pool
default-router 10.0.0.1
dns-server 10.0.0.1
network 10.0.0.0 255.255.255.0
```

```
ip dhcp pool 20pool
default-router 20.0.0.1
dns-server 20.0.0.1
network 20.0.0.0 255.255.255.0
```

```
ip dhcp pool 12pool
network 192.168.12.0 255.255.255.0
```


## Configuration - set DHCP client and relay agent on R2

```
interface g0/0
ip address dhcp 
```

```
interface g0/1
ip helper-address 20.0.0.1
```

Configure on PC
```
ipconfig /renew
```
