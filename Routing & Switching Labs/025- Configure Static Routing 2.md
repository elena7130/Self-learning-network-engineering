**Date:** 2026-02-2

**Topology:** 
<img width="1750" height="747" alt="image" src="https://github.com/user-attachments/assets/06fa3ac8-2142-41e7-8acc-fa5fdf5b1bf0" />


## Goal

- All IP addresses are preconfigured.
- Configure static routes on each router to allow full connectivity throughout the entire network.
- You have successfully completed the lab when each PC can ping any other point in the network.

  
## Configuration - on R1

```
ip route 10.0.2.0 255.255.255.0 192.168.12.2
ip route 10.0.3.0 255.255.255.0 192.168.13.3
ip route 10.0.4.0 255.255.255.0 192.168.12.2
```

## Configuration - on R2
```
ip route 10.0.1.0 255.255.255.0 192.168.12.1
ip route 10.0.3.0 255.255.255.0 192.168.12.1
ip route 10.0.4.0 255.255.255.0 192.168.24.4

```
## Configuration - on R3
```
ip route 10.0.1.0 255.255.255.0 192.168.13.1
ip route 10.0.2.0 255.255.255.0 192.168.13.1
ip route 10.0.4.0 255.255.255.0 192.168.34.4
```

## Configuration - on R4

```
ip route 10.0.1.0 255.255.255.0 192.168.24.2
ip route 10.0.2.0 255.255.255.0 192.168.24.2
ip route 10.0.3.0 255.255.255.0 192.168.34.3
```

