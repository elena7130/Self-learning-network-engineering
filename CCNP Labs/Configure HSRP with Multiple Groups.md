## Date :2026-3-11
## Goal :
Configure two Hot Standby Router Protocol (HSRP) groups, and verify the configuration.
1. On DSW1and DSW2, create two HSRP group with a group number of 10 and 20
2. The IP address of HSRP group 10 is 172.16.3.252 ; The IP address of HSRP group 20 is 172.16.3.254 ; 
3. Use HSRP 10 priority of 120 on DSW1 and  priority of 90 on DSW2 ;Use HSRP 20 priority of 120 on DSW2 and  priority of 90 on DSW1;

## Topology:
<img width="1036" height="396" alt="image" src="https://github.com/user-attachments/assets/6bd05598-48be-4511-815e-5127a7b83d95" />


## IP Address:
<img width="1902" height="1044" alt="image" src="https://github.com/user-attachments/assets/3070b203-14c2-457d-9868-872064c62c66" />


##  Configuration - On DSW1 and DSW2

```
DSW1(config)interface vlan 1
DSW1(config-vlan)standby 10 ip 172.16.3.252
DSW1(config-vlan)standby 10 priority 120
*By default, the switch with the highest priorit will become the active HSRP device.
DSW1(config-vlan)standby 10 preempt
DSW1(config-vlan)standby 20 ip 172.16.3.254
DSW1(config-vlan)standby 20 priority 90
DSW1(config-vlan)standby 20 preempt
*The reason we need preempt is that preemption is not enabled by default in an HSRP configuration, so we must switch with the highest priority become the new active device with the command, *
```


```
DSW2(config)interface vlan 1
DSW2(config-vlan)standby 10 ip 172.16.3.252
DSW2(config-vlan)standby 10 priority 90
DSW2(config-vlan)standby 10 preempt
DSW2(config-vlan)standby 20 ip 172.16.3.254
DSW2(config-vlan)standby 20 priority 120
DSW2(config-vlan)standby 20 preempt
```


##  Configuration - On ASW1 and ASW2

```
ASW1(config)ip default-gatway 172.16.3.252
```

```
ASW2(config)ip default-gatway 172.16.3.254
```

##  Configuration - On Client1 and Client2

```
Client1: ipconfig /dg 172.16.3.252
```

```
Client2:ipconfig /dg 172.16.3.254
```
