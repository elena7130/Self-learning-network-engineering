## Date : 2026-3-11

## Goals:

Plan, implement, and verify Open Shortest Path First (OSPF) operation over LAN interfaces and Frame Relay by using the point-to-point network type. You will also configure and verify OSPF operation for multiple areas.

## Topology:
<img width="858" height="720" alt="image" src="https://github.com/user-attachments/assets/f25438a1-692d-46f8-ac8d-5acc68914752" />

## IP Address 
<img width="1462" height="658" alt="image" src="https://github.com/user-attachments/assets/541b81e9-7fc3-4366-971f-fd887de89a48" />

## Steps1: Verify initial Configuration

1. Use commands `show ip interface brief ` and `show ip route` to verify the IP address  and state .
2. Verify connectivity with BBRouter1, BBRouter2, Router2, Router3, and Router4 by issuing a ping to the following interfaces:  

	BBRouter1’s Serial 0/0 interface – 172.30.1.1  
    BBRouter2’s Serial 0/0 interface – 172.30.1.5  
    Router2’s Serial 0/0 interface – 10.0.0.2  
    Router3’s Serial 0/0 interface – 10.0.0.10  
    Router4’s Serial 0/0 interface – 10.0.0.6

## Step2: Configure OSPF on Area 0 

```
Router1(config)interface loopback 0
Router1(config-if)ip address 1.1.1.1 255.255.255.0
Router1(config)router ospf 1 
router1(config-route)network 172.30.1.5 0.0.0.3 area 0
router1(config-route)network 172.30.1.0 0.0.0.3 area 0 
```


```
BBRouter1(config)interface loopback0
BBRouter1(config-if)ip add 11.11.11.11 255.255.255.0
BBRouter1(config)router ospf 1 
BBRouter1(config-route)network 172.30.1.0 0.0.0.3 area 0
```

```
BBRouter2(config)interface loopback0
BBRouter2(config-if)ip add 22.22.22.22 255.255.255.0
BBRouter2(config)router ospf 1 
BBRouter2(config-route)network 172.30.1.4 0.0.0.3 area 0
```


## Step3: Configure OSPF on Area 1

```
Router2(config)interface loopback 0 
ip add 2.2.2.2 255.255.255.0
router ospf 1 
network 10.0.0.0 0.0.0.3 area 1
network 10.3.0.0 0.0.0.255 area 1
```

```
Router3(config)interface loopback 0
ip add 3.3.3.3 255.255.255.0
```

```
Router4(config)interface loopback 0
ip add 4.4.4.4 255.255.255.0
router ospf 1
network 10.0.0.4 0.0.0.3 area 1
network 10.3.0.0 0.0.0.255 area 1
```

```
Router1(config)router ospf 1
network 10.0.0.0 0.0.0.3 area 1
network 10.0.0.4 0.0.0.3 area 1
```

## Step4: Configure OSPF on Area 2

```
Router1(config)router ospf 1
network 10.0.0.8 0.0.0.3 area 2
```


```
Router3(config)router ospf 1
network 10.0.0.8 0.0.0.3 area 2
network 10.5.0.0 0.0.0.255 area 2
```

Step5: Verify the OSPF database on Routers 

 Use command `show ip ospf database` and `show ip ospf neigbor` to examine the OSPF link-state database and neighbor. 


What is ABRs
What is LSAS 

