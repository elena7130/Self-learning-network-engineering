**Date:** 2026-02-03

**Topology:** 
<img width="1431" height="527" alt="image" src="https://github.com/user-attachments/assets/20616e32-1915-4055-9ea0-3129ee6e3890" />


## Goal
1. Configure multi-area OSPF as per the diagrams. Advertise all configured interfaces on router.(The loopbacks of R2, and R3 should be in Area 0)
    Configure the loopback interfaces as passive interfaces.
    Configure the reference bandwidth so that a 100-Gigabit interface would have a cost of 1.

2. Configure route summarization on the ABRs.
  
## Configuration - on R1 

```
interface loopback 0
ip address 1.1.1.1 255.255.255.255
router ospf 1
network 10.12.0.0 0.0.0.255 area 1
network 10.14.0.0 0.0.0.255 area 1
network 1.1.1.1 0.0.0.0 area 1
passive-interface loopback 0 
auto-cost reference bandwidth 10000
```

## Configuration - on R2
```
interface loopback 0
ip address 2.2.2.2 255.255.255.255
router ospf 1
network 10.12.0.0 0.0.0.255 area 1
network 10.23.0.0 0.0.0.255 area 0
network 1.1.1.1 0.0.0.0 area 0
passive-interface loopback 0 
auto-cost reference bandwidth 10000
```
## Configuration - on R3

```
interface loopback 0
ip address 3.3.3.3 255.255.255.255
router ospf 1
network 10.35.0.0 0.0.0.255 area 2
network 10.23.0.0 0.0.0.255 area 0
network 3.3.3.3 0.0.0.0 area 0
passive-interface loopback 0 
auto-cost reference bandwidth 10000
```

## Configuration - on R4

```
interface loopback 0
ip address 4.4.4.4 255.255.255.255
router ospf 1
network 10.14.0.0 0.0.0.255 area 0
network 4.4.4.4 0.0.0.0 area 0
passive-interface loopback 0 
auto-cost reference bandwidth 10000
```


## Configure route summarization on the ABRs.

* On R3 and R2
```
area 0 rage 10.0.0.0 255.0.0.0
# the mac address is regular mac address rather than wild card addreess
```
