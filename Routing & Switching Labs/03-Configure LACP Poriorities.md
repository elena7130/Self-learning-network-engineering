## Goal : 

1. Change the priority on the FastEthernet 0/9 to 100
2. Change the priority on the system

### **Topology**
<img width="1280" height="192" alt="image" src="https://github.com/user-attachments/assets/be5fb581-6b96-45c6-8876-ab0cf264175e" />


## Configuration - change the priority on the port 

```
Asw1(config)interface f 0/9
Asw1(config-if)lacp port-priority 100

## By configuring a port priority lower than the other interfaces, you can make sure that FastEthernet 0/9 is selected as an active interface and not placed in hot standby. LACP port priorities can be configured in the range from 1 through 65535. The lower the value, the higher the priority. Therefore, configuring the FastEthernet 0/9 interface with a value lower than the default value of 32768 should ensure that the FastEthernet 0/9 interface has a higher priority than interfaces configured with the default value.
```

## Configuration - priority on the system

```
Asw1(config)lacp system-priority 100
# By changing the LACP system priority value on ASW1, I can configure it to be the decision maker for active ports in the EtherChannel.
```

## Vertify

The output of the show etherchannel summary command now indicates that FastEthernet 0/9 is bundled (indicated by the P flag). The FastEthernet 0/8 interface, on the other hand, has been placed in hot standby (indicated by the H flag).
