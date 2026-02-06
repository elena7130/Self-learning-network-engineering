**Date:** 2026-02-02

**Topology:** 
<img width="738" height="693" alt="image" src="https://github.com/user-attachments/assets/ef3883b9-79a4-4782-aab5-63770cddf189" />


## Goal：

This lab begins with several key features pre-configured. Make sure to pay close attention to the initial configurations to get your bearings before starting to do the lab. These items are preconfigured:

- The links connecting the Access switches with their Distribution switches are preconfigured as static trunks using 802.1q encapsulation.
- The access and distribution switches have been pre-configured with the VLAN IDs listed in the figure.
- All interfaces shown in the figure have been administratively enabled.
- Layer 3 switches Dist1 and Dist2 have been pre-configured with OSPF so that once the lab has been configured, Dist1 and Dist2 will exchange IPv4 routes.

The following list details your work for this lab:

- Configure Layer 3 switching with SVIs on the two distribution switches as follows:
    - Switch Dist1 routes for VLANs 10 and 20
    - Switch Dist2 routes for VLANs 30 and 40
- Configure a layer 3 EtherChannel for the two links between switches Dist1 and Dist2 so that IPv4 packets can be routed between the two switches, as follows:
    - Configure the two links between the distribution switches as a static layer 3 EtherChannel with port-channel interface number 10.
    - Make the EtherChannel a routed port instead of a switch port.
    - Configure the IP addresses per the figure for the PortChannel interface

## Configuration 

1. Checking the existed configuration on Dist 1 and Dist using `show interface trunking`and`show ip interface brief`
2. After I verity , I find that the interface G1/1/3 has been trunk port . 
3. Configuring the SVI on Dist 1 and Dist 2 

```
vlan 10
interface vlan 10
ip address 10.100.100.1 255.255.255.224
vlan 20
interface vlan 20
ip address 10.100.100.14 255.255.255.224
```

```
vlan 30
interface vlan 30
ip add 10.100.100.65 255.255.255.224
vlan 40
interface vlan 40
ip add 10.100.100.97 255.255.255.224
```

4. Configuring the EtherChannel and ip address on Dist 1 
```
Dist1(config)interface range g1/1/1 -2
Dist1(config-if-range)channel group 10 mode on
Dist1(config-if-range)no switchport
Dist1(config-if-range)interface port-channel 10
Dis1t(config-if-range)ip address 100.1.12.1 255.255.255.240
```

```
Dist2(config)interface range g1/1/1 -2
Dist2(config-if-range)channel group 10 mode on
Dist2(config-if-range)no switchport
Dist2(config-if-range)interface port-channel 10
Dist2(config-if-range)ip address 100.1.12.14 255.255.255.240
```

*Lab Resource* : https://www.certskills.com/clab554/#1621529957898-a5fb3bce-f3aa
