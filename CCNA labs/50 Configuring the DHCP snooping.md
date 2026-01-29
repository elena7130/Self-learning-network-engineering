
## Goal:

1. Configure R1 as a DHCP server. 
    Exclude 192.168.1.1 - 192.168.1.9 from the pool; 
    Default gateway: R1

2. Configure DHCP snooping on SW1 and SW2.
    Configure the uplink interfaces as trusted ports.

 
## Topology
<img width="986" height="340" alt="image" src="https://github.com/user-attachments/assets/1e7cbcaa-f1c8-4dad-9237-abb0696ccc5a" />



## Configuration - DHCP pools on R1(DHCP server)

```
R1(config)#ip dhcp exclued-address 192.168.1.1 192.168.1.9
R1(config)#ip dhcp pool pool1
R2(dhcp-config)#network 192.168.1.0 255.255.255.0
R2(config)#defalut-router 192.168.1.1
# set pool1
```

## Configuration - DHCP spooning on SW1 and SW2

```
SW1(config)#ip dhcp snooping
SW1(config)#ip dhcp snooping vlan 1
SW1(config)#no ip dhcp snooping information option
## Why use this configuration , because DHCP relay agents can option 82 to message they froward to the remote DHCP server
so ,by default , Cisco switches will drop DHCP message with Option 82 that are trust reccieve on untrust. 
SW1(config)#int g0/2
SW1(config-if)#ip dhcp snooping trust 

SW2(config)#ip dhcp snooping
SW2(config)#ip dhcp snooping vlan 1
SW2(config)#no ip dhcp snooping information option
SW2(config)#int g0/1
SW2(config-if)#ip dhcp snooping trust 

```


## Configuration - CLI(on PC1-PC3)

```
c:\> ipconfig / all
c:\> ipconfig / release 
c:\> ipconfig / revew 
```

