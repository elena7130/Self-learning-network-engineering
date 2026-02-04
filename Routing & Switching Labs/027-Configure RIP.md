**Date:** 2026-02-4

**Topology:** 
<img width="1436" height="572" alt="image" src="https://github.com/user-attachments/assets/28b1dda4-25c8-4567-b0f2-4e25d54770b9" />



## Goal

The network has been preconfigured according to the diagram.
Configure RIPv2 on each router to allow full connectivity throughout the network.
Disable routing updates on interfaces connected to switches.

  
## Configuration - on R1

```
interface loopback 0 
ip address 1.1.1.1 255.255.255.255
router rip 
version 2
network 1.1.1.1
network 10.0.0.0
network 13.0.0.0
network 12.0.0.0
passive-interface loopback 0
```

## Configuration - on R2
```
interface loopback 0 
ip address 2.2.2.2 255.255.255.255
router rip 
version 2
network 2.2.2.2
network 24.0.0.0
network 20.0.0.0
network 12.0.0.0
passive-interface loopback 0

```
## Configuration - on R3
```
interface loopback 0 
ip address 3.3.3.3 255.255.255.255
router rip 
version 2
network 3.3.3.3
network 30.0.0.0
network 34.0.0.0
network 13.0.0.0
passive-interface loopback 0
```

## Configuration - on R4

```
interface loopback 0 
ip address 4.4.4.4 255.255.255.255
router rip 
version 2
network 4.4.4.4
network 24.0.0.0
network 40.0.0.0
network 34.0.0.0
passive-interface loopback 0
```

