**Date:** 2026-01-29

**Topology:** 
<img width="1184" height="223" alt="image" src="https://github.com/user-attachments/assets/76428de9-5312-4327-a463-12a60dbbe944" />


## Goal:

1. Configure a Layer 2 EtherChannel between SW1 and SW2 using a Cisco proprietary protocol. Configure the EtherChannel as a trunk 
2. Configure a Layer 3 EtherChannel between SW2 and SW3. Configure it as a static EtherChannel. Configure the appropriate IP addresses.
3. Configure a Layer 2 EtherChannel between SW3 and SW4 using an IEEE standard protocol. Configure the EtherChannel as a trunk.
  
## Configuration

1. Configure on SW1 and SW2 (Layer 2)

```
SW1(config)interface range f0/1 - 4
SW1(config-if-range)channel-group 1 mode desirable
# using PAgP mode 
SW1(config-if-range)interface port-channel 1
SW1(config-if)interface port-channel 1
SW1(config-if)switchport mode trunk 

SW2(config)interface range f0/1 - 4
SW2(config-if-range)channel-group 1 mode desirable
SW2(config-if-range)interface port-channel 1
SW2(config-if)interface port-channel 1
SW2(config-if)switchport mode trunk 
```


2. Configure on SW2 and SW3 (Layer 3)
```
SW2(config)interface range g0/1 - 2
SW2(config-if-range)no switchport
SW2(config-if-range)channel-group 2 mode on
# using static mode 
SW2(config-if-range)interface port-channel 2
SW2(config-if)ip add 23.0.0.1 255.255.255.252

SW3(config)interface range g0/1 - 2
SW3(config-if-range)no switchport
SW3(config-if-range)channel-group 2 mode on
SW3(config-if-range)interface port-channel 2
SW3(config-if)ip add 23.0.0.2 255.255.255.252

```

3. Configure on SW3 and SW4 (Layer 3)

```
SW3(config)interface range f0/1 - 4
SW3(config-if-range)channel-group 1 mode active
# using LACP mode 
SW3(config-if-range)interface port-channel 1
SW3(config-if)interface port-channel 1
SW3(config-if)switchport mode trunk 

SW4(config)interface range f0/1 - 4
SW4(config-if-range)channel-group 1 mode active
SW4(config-if-range)interface port-channel 1
SW4(config-if)interface port-channel 1
SW4(config-if)switchport mode trunk 
```

4. Configure-checking
```
SW1(config)do etherchannel summary
```
