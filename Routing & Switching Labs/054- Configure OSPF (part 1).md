**Date:** 2026-02-03

**Topology:** 
<img width="1171" height="497" alt="image" src="https://github.com/user-attachments/assets/8bcc69f3-cae1-4eee-8b64-dd44ebfbc88d" />



## Goal

1. Configure a loopback address on each router (1.1.1.1/32 for R1, 2.2.2.2/32 for R2, etc.)
2. Configure OSPF on each router. Advertise all interfaces, including the loopback.
3. Suppress OSPF messages on each router's loopback interface.
4. Configure the OSPF reference bandwidth of each router so that a 10-GigabitEthernet interface would have an OSPF cost of 1.

  
## Configuration - on R1 

```
interface loopback 0
ip address 1.1.1.1 255.255.255.255
router ospf 1
network 12.0.0.0 0.0.0.255 area 0
network 12.0.0.0 0.0.0.255 area 0
network 1.1.1.1 0.0.0.0 area 0
passive-interface loopback 0 
```

## Configuration - on R2
```
interface loopback 0
ip address 2.2.2.2 255.255.255.255
router ospf 1 # the process ID can different with the neighbour's
network 12.0.0.0 0.0.0.255 area 0
network 23.0.0.0 0.0.0.255 area 0
network 2.2.2.2 0.0.0.0 area 0
passive-interface loopback 0 

```
## Configuration - on R3

```
interface loopback 0
ip address 3.3.3.3 255.255.255.255
router ospf 1
network 34.0.0.0 0.0.0.255 area 0
network 23.0.0.0 0.0.0.255 area 0
network 3.3.3.3 0.0.0.0 area 0
passive-interface loopback 0 
```

## Configuration - on R4

```
interface loopback 0
ip address 4.4.4.4 255.255.255.255
router ospf 1
network 14.0.0.0 0.0.0.255 area 0
network 34.0.0.0 0.0.0.255 area 0
network 4.4.4.4 0.0.0.0 area 0
passive-interface loopback 0 
```


## Configure the OSPF reference bandwidth

On R1-R4
```
router ospf 1
auto-cost reference bandwidth 10000
```
