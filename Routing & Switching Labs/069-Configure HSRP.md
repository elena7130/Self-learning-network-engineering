## Date : 2026-2-12
## **Topology:** 

<img width="1048" height="706" alt="image" src="https://github.com/user-attachments/assets/484888e7-ddf9-4df3-8f32-817f1e02c41f" />



## Goal:
1. Configure HSRP with the following requirements:
    -use HSRP version 2
    -use .1 as the virtual IP for each VLAN (10.10.10.1, 10.20.20.1)
    -R1 is the active for VLAN10, standby for VLAN20
    -R2 is active for VLAN20, standby for VLAN10
    -Enable preemption
## Configuration - on R1

```
R1(config)interface g0/1
R1(config-if)standby version2
R1(config-if)standby 10 ip 10.10.10.1
R1(config-if)standby 10 priority 150 (100 is default)
R1(config-if)standby 10 preempt
```

```
R1(config)interface g0/2
R1(config-if)standby version2
R1(config-if)standby 20 ip 10.20.20.1
R1(config-if)standby 20 preempt
```

## Configuration - on R2

```
R2(config)interface g0/1
R2(config-if)standby version2
R2(config-if)standby 20 ip 10.20.20.1
R2(config-if)standby 20 priority 150 (100 is default)
R2(config-if)standby 20 preempt
```

```
R2(config)interface g0/2
R2(config-if)standby version2
R2(config-if)standby 10 ip 10.10.10.1
R2(config-if)standby 10 preempt
```

