**Date:** 2026-01-30

**Topology:** 
<img width="1021" height="560" alt="image" src="https://github.com/user-attachments/assets/9f2ffb5f-957a-4894-b682-20ce706896da" />



## Goal

1. Configure the hostnames of R1, SW1, and SW2 according to the diagram.

2. Configure an enable secret of 'CCNA' for each networking device.

3. Configure the switchports to which PCs are connected as access ports in the following VLANS:
    VLAN13: PC1, PC3
    VLAN24: PC2, PC4

4.  configure a trunk link between SW1 and SW2.

5. Configure port security on the switchports connected to PCs, with the following settings:
    -sticky MAC address learning enabled
    -violation action: 'restrict'

6. Configure inter-VLAN routing with the 'router on a stick' method, according to the network diagram and the following subinterface addresses:
    VLAN13: 10.0.0.1
    VLAN24: 10.0.1.1
7. Ping between the PCs to confirm full connectivity, including between different VLANs.
  

## Configuration:

1&2 . Configure hostname and secret on R1,SW1,SW2
 
```
Router(config)hostname R1
R1(config-if)enable secret CCNA

```

```
Switch(config)hostname SW1
SW1(config-if)enable secret CCNA
```

```
Switch(config)hostname SW2
SW2(config-if)enable secret CCNA
```

3.  Configure VLANs 
```
SW1(config)interface f0/2
SW1(config-if)switchport access vlan 13
SW1(config)interface f0/3
SW1(config-if)switchport access vlan 24
```

```
SW2(config)interface f0/2
SW2(config-if)switchport access vlan 13
SW2(config)interface f0/3
SW2(config-if)switchport access vlan 24
```

4.  Configure Trunks
```
SW1(config)interface f0/1
SW1(config-if)switchport mode trunk 
SW1(config-if)switchport trunk native vlan 1001
SW1(config-if)switchport trunk allowed vlan 13,24
SW1(config)do show vlan brief
```

```
SW2(config)interface f0/1
SW2(config-if)switchport mode trunk 
SW2(config-if)switchport trunk native vlan 1001
SW2(config-if)switchport trunk allowed vlan 13,24
SW2(config)do show vlan brief

```

5. Configure port security
```
SW1(config)interface range f0/2-3
SW1(config-if-range)switchport mode access
SW1(config-if-range)switchport port-security 
SW1(config-if-range)switchport port-security mac-address stricky
SW1(config-if-range)switchport port-security violation restrict
```

```
SW2(config)interface range f0/2-3
SW2(config-if-range)switchport mode access
SW2(config-if-range)switchport port-security 
SW2(config-if-range)switchport port-security mac-address stricky
SW2(config-if-range)switchport port-security violation restrict
```

6. Configure inter-VLAN routing with the 'router on a stick'
```
R1(config)interface g0/0
R1(config-subif)no shutdown
R1(config-subif)interface g0/0.13
R1(config-subif)encapsulation dot1Q 13
R1(config-subif)ip address 10.0.0.1 255.255.255.0
R1(config-subif)interface g0/0.24
R1(config-subif)encapsulation dot1Q 243
R1(config-subif)ip address 10.0.1.1 255.255.255.0
```

7. Checking on PC 
   ping 10.0.0.13 and ping 10.0.1.14 on PC1
