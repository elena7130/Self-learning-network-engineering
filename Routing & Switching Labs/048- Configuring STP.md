**Date:** 2026-01-26
**Topology:** 
<img width="1169" height="741" alt="image" src="https://github.com/user-attachments/assets/75309f88-11b7-4ac9-9568-21e9a22443b7" />


## Goals

- 1. What is the current (default) STP version running on the switches?
    What is the bridge ID for each switch?
    What is the root bridge for each VLAN?
    What is the STP cost of each interface?
    Which interface is blocked? Why?

2. Change the spanning-tree mode on each switch to RPVST.

3. Make the following configurations:
    VLAN10 Root: SW1, Secondary Root: SW2
    VLAN20 Root: SW2, Secondary Root: SW3
    VLAN30 Root: SW3, Secondary Root: SW1

4. Enable Portfast and BPDU Guard on the appropriate interfaces.
  
Steps: 

[Answer1]
2. Configuration-on each switch 
```
SW1#show spanning-tree
```

the bridge on SW1 on VLAN0001:32769
the bridge on SW1 on VLAN0010:32778  
the bridge on SW1 on VLAN0020:32788  
the bridge on SW1 on VLAN0020:32798 

the bridge on SW2 on VLAN0001:32769
the bridge on SW2 on VLAN0010:32778  
the bridge on SW2 on VLAN0020:32788  
the bridge on SW2 on VLAN0020:32798 

the bridge on SW3 on VLAN0001:32769   
the bridge on SW3 on VLAN0010:32778  
the bridge on SW3 on VLAN0020:32788  
the bridge on SW3 on VLAN0020:32798 

---------
 
 3.the root bridge for VLAN10/20/30 is SW2

---------

4.the STP cost of interface on SW2
Use the configuration 'show spanning-tree '

------ 
5.The interface g0/1 on SW1 is blocked , because the interface is alternative port ;


### Answer 2 :
Configure on SW1/2/3

```
SW1(config)spanning-tree mode rapid-pvst
#The same configuration on SW2 and SW3
```


### Answer 3 :

Configure on SW1/2/3

```
SW1(config)spanning-tree vlan 10 root primary
SW1(config)spanning-tree vlan 30 root secondary
SW2(config)spanning-tree vlan 20 root primary
SW2(config)spanning-tree vlan 10 root secondary
SW3(config)spanning-tree vlan 30 root primary
SW3(config)spanning-tree vlan 20 root secondary
```

Answer 4 :
```
SW1(config)intface range f0/1 - 3
SW1(config-if-range)spanning-tree portfast 
SW1(config-if-range)spanning-tree bpduguard enable
SW2(config)spanning-tree portfast default
SW2(config-if-range)spanning-tree bpduguard default
SW3(config)spanning-tree portfast default
SW3(config-if-range)spanning-tree bpduguard default
```
