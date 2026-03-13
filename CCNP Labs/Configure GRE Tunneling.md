## Date : 2026/3/13
## Goal:

Configure GRE tunneling between R1 and R3 to connect PC1 and PC2

## Topology
<img width="462" height="642" alt="image" src="https://github.com/user-attachments/assets/faa22e19-b1b6-4ebc-9a7e-4a3b3fa3cc9c" />


## IP Address:
<img width="1470" height="730" alt="image" src="https://github.com/user-attachments/assets/7920d60a-19e2-423f-b535-d9f40a47eba2" />


## Background:

1. All of IP addresses have configured on the interfaces . 
2. Except the connect The router tables on R1 just have static route to s0/0 on R2 .At the same time , in  the R3 , there is only static router to s0/1 on R3 . So , now we can't ping from PC1 to PC3 , because we have no routing to each other.

## Configuration :

1. Create a new tunnel and IP address on R1 and R3 

```
R1(config)interface tunnel 0
R1(config-if)tunnel source 198.51.100.1
R1(config-if)tunnel destination 198.51.100.6
R1(config-if)ip address 192.168.0.1 255.255.255.252

R3(config)interface tunnel 0
R3(config-if)tunnel source 198.51.100.6
R3(config-if)tunnel destination 198.51.100.1
R3(config-if)ip address 192.168.0.2 255.255.255.252
```

2. Verify tunnels , we can through  `show ip interface brief `to verify the state and protocols of tunnels are all up and up .

3. Try to create state route to 10.10.10.0/24 and 10.10.30.0/24 network through tunnel on each Router  

```
R1(config)ip route 10.10.30.0 255.255.255.0 192.168.0.2

R3(config)ip route 10.10.10.0 255.255.255.0 192.168.0.1
```

4. Remove the state route , try to build OSPF through tunnel on each router.

```
R1(config)router ospf 1
R1(config-route)network 10.10.10.0  0.0.0.255  area 0 
R1(config-route)network 192.168.0.0  0.0.0.3  area 0

R3(config)router ospf 1
R3(config-route)network 10.10.30.0  0.0.0.255  area 0 
R3(config-route)network 192.168.0.0  0.0.0.3  area 0

```

5. Verify 

Now , PC1 can ping PC3 successfully . Also , we can find  `10.10.30.0/24 [110/11112] via 192.168.0.2, 00:00:42, Tunnel0` in the router table . At the same time , I use `show ip ospf neighbor` on R1 and R3 can confirms a full adjacency with the remote peer over the Tunnel IP.
