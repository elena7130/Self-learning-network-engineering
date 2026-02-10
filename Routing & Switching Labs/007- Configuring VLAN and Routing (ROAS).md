**Date:** 2026-02-10

**Topology:** 

<img width="1220" height="660" alt="image" src="https://github.com/user-attachments/assets/6890bbce-e646-4469-818f-57c623138107" />


## Goal:

1. Ping between the PCs. Which pings succeed?
2. Assign PC1 and PC3 to VLAN 13, and PC2 and PC4 to VLAN 24.
3. Create a trunk link between SW1 and SW2.
4. Configure inter-VLAN routing by using subinterfaces on R1's G0/0 interface. Use an address of 10.0.0.1/25 for VLAN 13 and 10.0.0.129/25 for VLAN 24.
5. Test connectivity by pinging between PCs.
  
## A1:

Before configuring , PC1(10.0.0.2) can ping PC3(10.0.0.3)  successfully , because they are in the same Lan with the same default gateway.

## Configuration -- VLANs

```
SW1(config)int f0/2
SW1(config-if)switchport access vlan 24
SW1(config)int f0/1
SW1(config-if)switchport access vlan 13
```

```
SW2(config)int f0/2
SW2(config-if)switchport access vlan 24
SW2(config)int f0/1
SW2(config-if)switchport access vlan 13
```

```
show vlan brief
show interface trunking
```
## Configuration -- a trunk link

```
SW1(config)interface g0/1
SW1(config-if)switchport mode trunk
SW1(config-if)switchport trunk native vlan 1001
SW1(config-if)switchport trunk allow vlan 13,24
```

```
SW2(config)interface range g0/1-2
SW2(config-if-range)switchport mode trunk
SW2(config-if-range)switchport trunk native vlan 1001
SW2(config-if-range)switchport trunk allow vlan 13,24
```

## Configuration -- ROAS

```
R1(config)interface g0/0
R1(config-if)no shutdown
R1(config)interface g0/0.13
R1(config-subif)encapulation dot1Q 13
R1(config-subif)ip add 10.0.0.1 255.255.255.128
R1(config)interface g0/0.24
R1(config-subif)encapulation dot1Q 24
R1(config-subif)ip add 10.0.0.129 255.255.255.128
```

PCs can ping each others. 
