## Data : 2026-3-3
## Objective

Plan, implement, and verify Open Shortest Path First (OSPF) operation over LAN interfaces, Frame Relay using the point-to-point network type, and Layer 3 switches. You will also configure and verify OSPF operation for multiple areas and explore alternate OSPF configuration mechanisms

## Topology 

<img width="1018" height="586" alt="image" src="https://github.com/user-attachments/assets/b944ce9c-10c5-43a5-99f2-ec2981c3de81" />


## IP Addresses

| Divice     | Interface                                                                  | IP addree                                                             | Subnet Mask                                                                                         |     |
| ---------- | -------------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- | --- |
| BBR1       | Serial 0/0.101  <br>Serial 0/0.201  <br>Serial 0/0.301  <br>Serial 0/0.401 | 12.0.0.1  <br>12.0.0.5  <br>12.0.0.9  <br>12.0.0.13                   | 255.255.255.252  <br>255.255.255.252  <br>255.255.255.252  <br>255.255.255.252                      |     |
| CoreR1     | Serial 0/0  <br>FastEthernet 1/0                                           | 12.0.0.2  <br>12.1.0.1                                                | 255.255.255.252  <br>255.255.255.252                                                                |     |
| CoreR2<br> | Serial 0/0  <br>FastEthernet 1/0                                           | 12.0.0.6<br>12.2.0.1                                                  | 255.255.255.252  <br>255.255.255.252                                                                |     |
| CoreR3     | Serial 0/0  <br>FastEthernet 1/0                                           | 12.0.0.10  <br>12.3.0.1                                               | 255.255.255.252  <br>255.255.255.252                                                                |     |
| CoreR4     | Serial 0/0  <br>FastEthernet 1/0                                           | 12.0.0.14  <br>12.4.0.1                                               | 255.255.255.252  <br>255.255.255.252                                                                |     |
| DSW1       | FastEthernet 0/1  <br>VLAN 11  <br>VLAN 12  <br>VLAN 13  <br>VLAN 14       | 12.1.0.2  <br>12.1.1.1  <br>12.1.1.65  <br>12.1.1.129  <br>12.1.1.193 | 255.255.255.252  <br>255.255.255.192  <br>255.255.255.192  <br>255.255.255.192  <br>255.255.255.192 |     |
| DSW2       | FastEthernet 0/1  <br>VLAN 21  <br>VLAN 22  <br>VLAN 23  <br>VLAN 24       | 12.2.0.2  <br>12.2.1.1  <br>12.2.1.65  <br>12.2.1.129  <br>12.2.1.193 | 255.255.255.252  <br>255.255.255.192  <br>255.255.255.192  <br>255.255.255.192  <br>255.255.255.192 |     |
| DSW3       | FastEthernet 0/1  <br>VLAN 31  <br>VLAN 32  <br>VLAN 33  <br>VLAN 34       | 12.3.0.2  <br>12.3.1.1  <br>12.3.1.65  <br>12.3.1.129  <br>12.3.1.193 | 255.255.255.252  <br>255.255.255.192  <br>255.255.255.192  <br>255.255.255.192  <br>255.255.255.192 |     |
| DSW4       | <br>FastEthernet 0/1  <br>VLAN 41  <br>VLAN 42  <br>VLAN 43  <br>VLAN 44   | 12.4.0.2  <br>12.4.1.1  <br>12.4.1.65  <br>12.4.1.129  <br>12.4.1.193 | 255.255.255.252  <br>255.255.255.192  <br>255.255.255.192  <br>255.255.255.192  <br>255.255.255.192 |     |
| ASW1       | VLAN 11                                                                    | 12.1.1.2                                                              | 255.255.255.0                                                                                       |     |
| ASW2       | VLAN 21                                                                    | 12.2.1.2                                                              | 255.255.255.0                                                                                       |     |
| ASW3       | VLAN 31                                                                    | 12.3.1.2                                                              | 255.255.255.0                                                                                       |     |
| ASW4       | VLAN 41                                                                    | 12.4.1.2                                                              | 255.255.255.0                                                                                       |     |

## Task 1: Plan for Multi-Area OSPF
  
1. Each Serial 0/0 subinterface on BBR1 and each Serial 0/0 interface on CoreR1, CoreR2, CoreR3, and CoreR4 should be configured as members of the backbone. Your configuration should be specific enough so that as additional networks are added to the router, those networks are not automatically advertised. The IP routing tables on each router should be populated with the specific IP subnets in your network. Using the IP Addresses tables, list the specific networks and subnet masks, using Classless Inter-Domain Routing (CIDR) notation, that should be configured so that only those specific interfaces run OSPF.

    BBR1:  Network In Area 0 
      12.0.0.0  255.255.255.252
      12.0.0.4  255.255.255.252
      12.0.0.8  255.255.255.252
      12.0.0.12  255.255.255.252
    CoreR1:  Network In Area 0 
      12.0.0.0  255.255.255.252
    CoreR2:  Network In Area 0 
      12.0.0.4 255.255.255.252
    CoreR3:   Network In Area 0 
      12.0.0.8 255.255.255.252
    CoreR4: Network In Area 0 
      12.0.0.12 255.255.255.252
  

2. The following interfaces should run OSPF in Area 1:
    CoreR1: FastEthernet 1/0  
    DSW1: FastEthernet 0/1 and each Switched Virtual Interface (SVI) that is configured with an IP address

    CoreR1:  12.1.0.0 /30
    DSW1: 12.1.0.0/30    12.1.1.0/26  12.1.1.64/26  12.1.1.128/26  12.1.1.192 / 26  

3.   The following interfaces should be configured to run OSPF in Area 2:  
  
CoreR2: FastEthernet 1/0  
DSW2: FastEthernet 0/1 and each SVI that is configured with an IP address

     CoreR2:12.2.0.0/30
     DSW2: 12.2.0.0/30 , 12.2.1.0/26 , 12.2.1.64/26 ,12.2.1.128/26 ,12.2.1.192/26


4.The following interfaces should be configured to run OSPF in Area 3:  
  
CoreR3: FastEthernet 1/0  
DSW3: FastEthernet 0/1 and each SVI that is configured with an IP address 

    CoreR3: 
    DSW3:


5.The following interfaces should be configured to run OSPF in Area 4:  
  
CoreR4: FastEthernet 1/0  
DSW4: FastEthernet 0/1 and each SVI that is configured with an IP address

     CoreR4:12.4.0.0/30
     DSW4:12.4.0.0/30 , 12.4.1.0/26 , 12.4.1.64/26, 12.4.1.128/26 , 12.4.1.192/26


## Configuration on BBR1 and Core R1 - R4

```
BBR1(config)router ospf 1
BBR1(config-route)router-id 1.0.0.1

#If you don’t specify a router ID, OSPF will pick the highest IP address of your loopback interfaces. If you don’t have loopback interfaces, it will pick the highest IP address on any of your physical interfaces. Once a router ID has been selected, it won’t change until you reset the OSPF process.

BBR1(config-route)network 12.0.0.0 0.0.0.15 area 0 
```

```
CoreR1(config)router ospf 1
CoreR1(config-route)router-id 1.1.1.1
CoreR1(config-route)intface s0/0
CoreR1(config-if)ip ospf 1 area 0
CoreR1(config-if)intface f1/0
CoreR1(config-if)ip ospf 1 area 1
```

```
CoreR2(config)router ospf 1
CoreR2(config-route)router-id 1.2.1.1
CoreR2(config-route)intface s0/0
CoreR2(config-if)ip ospf 1 area 0
CoreR2(config-if)intface f1/0
CoreR2(config-if)ip ospf 1 area 2
```

```
CoreR3(config)router ospf 1
CoreR3(config-route)router-id 1.3.1.1
CoreR3(config-route)intface s0/0
CoreR3(config-if)ip ospf 1 area 0
CoreR3(config-if)intface f1/0
CoreR3(config-if)ip ospf 1 area 3
```

```
CoreR4(config)router ospf 1
CoreR4(config-route)router-id 1.4.1.1
CoreR4(config-route)intface s0/0
CoreR4(config-if)ip ospf 1 area 0
CoreR4(config-if)intface f1/0
CoreR4(config-if)ip ospf 1 area 4
```

## Configuration on DSW1-DSW4

```
DSW1(config)ip routing
DSW1(config)router ospf 1
DSW1(config-router)router-id 1.1.0.1
DSW1(config-router)network 12.1.1.0 0.0.0. area 1
DSW1(config-router)passive-interface vlan 11
DSW1(config-router)passive-interface vlan 12
DSW1(config-router)passive-interface vlan 13
DSW1(config-router)passive-interface vlan 14
DSW1(config-router)ineterface f0/1
DSW1(config-if)ip ospf 1 area 1
```

```
DSW2(config)ip routing
DSW2(config)router ospf 1
DSW2(config-router)router-id 1.2.0.1
DSW2(config-router)network 12.2.1.0 0.0.0. area 2
DSW2(config-router)passive-interface vlan 21
DSW2(config-router)passive-interface vlan 22
DSW2(config-router)passive-interface vlan 23
DSW2(config-router)passive-interface vlan 24
DSW2(config-router)ineterface f0/1
DSW2(config-if)ip ospf 1 area 2
```

```
DSW3(config)ip routing
DSW3(config)router ospf 1
DSW3(config-router)router-id 1.3.0.1
DSW3(config-router)network 12.3.1.0 0.0.0. area 3
DSW3(config-router)passive-interface vlan 31
DSW3(config-router)passive-interface vlan 32
DSW3(config-router)passive-interface vlan 33
DSW3(config-router)passive-interface vlan 34
DSW3(config-router)ineterface f0/1
DSW3(config-if)ip ospf 1 area 3
```

```
DSW4(config)ip routing
DSW4(config)router ospf 1
DSW4(config-router)router-id 1.4.0.1
DSW4(config-router)network 12.4.1.0 0.0.0. area 4
DSW4(config-router)passive-interface vlan 41
DSW4(config-router)passive-interface vlan 42
DSW4(config-router)passive-interface vlan 43
DSW4(config-router)passive-interface vlan 44
DSW4(config-router)ineterface f0/1
DSW4(config-if)ip ospf 1 area 4
```


## Verify on BBR1

Using `show ip ospf database`,`show ip ospf interface brief` ,`show ip ospf neighbour` to verify configurations are correct . And, on the BBR1 , I should ping the pcs in different VLAN successfully on BBR1 . 

# This lab was built and tested using the NetSim online lab environment.
