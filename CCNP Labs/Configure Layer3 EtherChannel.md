## Goal :
You will plan, implement, and verify Layer 3 EtherChannel configurations in this lab .

## Topology

<img width="846" height="290" alt="image" src="https://github.com/user-attachments/assets/0ffa3baa-b631-4b4b-845d-6fb015f4e1e9" />


## Steps 1 :Planning

1. What advantage would you gain by using layer 3 EtherChannel ?
    In addition to IP load balancing and bandwidth scalability, Layer 3 EtherChannel can be advantageous in scenarios where you would like to achieve Layer 3 connectivity between switches but keep Spanning Tree Protocol (STP) and other control traffic isolated.
  
2. List some factors that you should consider when selecting which load balancing method to apply. 

    EtherChannel supports several different methods for load balancing traffic across bundled links. You should select the load balancing method that will provide you with the best distribution among links based on the network traffic. If, for example, most of your traffic is destined for a single IP address, selecting the dst-ip method could result in the same interface being selected each time. You might instead choose a method that involves the source Media Access Control (MAC) or source IP address when selecting a link.

## Step2 :Initial Configurations

1.    DSW1 and DSW2, issue the command to determine the number of links that can be configured as part of the port-channel group.
    `show cdp neighbor`

2. On DSW1 and DSW2, issue the command to display the line and protocol state of each interface.
   `show ip interface brief` 

3.  On DSW1 and DSW2, issue the command to display information about Layer 3 protocols running on each device. Is IP routing currently enabled on DSW1 and DSW2? 
    `show protocols`

## Step3 : Configure IP Routing 

```
DSW1(config)ip routing
DSW1(config)route eigrp 100
DSW1(config-route)auto-summary
DSW1(config-route)network 172.16.0.0
# ip address of vlan 12 on the DSW2 is 172.16.12.200
```

```
DSW2(config)ip routing
DSW2(config)route eigrp 100
DSW2(config-route)auto-summary
DSW2(config-route)network 172.16.0.0
# ip address of vlan 11 on the DSW1 is 172.16.11.100 
```

## Step4 : Configure layer3 EtherChannel 

```
DSW1(config)interface range f0/5 - 6 
DSW1(config-if-range)no switchport
DSW1(config-if-range)channel-group 1 mode on
DSW1(config)interface port-channel 1
DSW1(config)ip address 172.16.1.1 255.255.255.252
```

```
DSW2(config)interface range f0/5 - 6 
DSW2(config-if-range)no switchport
DSW2(config-if-range)channel-group 1 mode on
DSW2(config)interface port-channel 1
DSW2(config)ip address 172.16.1.1 255.255.255.252
```

## Step5 : Vertify

```
show etherchannel summary
## The interface f0/5 and f0/6 should in the etherchannel group 1 and the state should be RU and P (RU means layer3 etherchannel in use / P means bundled in port-channel)
```
