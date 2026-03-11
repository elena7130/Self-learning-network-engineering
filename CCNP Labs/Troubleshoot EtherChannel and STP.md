## Date :2026-3-10
## Goals:
Troubleshooting an EtherChannel configuration.

## Topology :
<img width="844" height="122" alt="image" src="https://github.com/user-attachments/assets/907a796c-3936-49ea-a3c7-8be27a9fce62" />


## Steps 1: Examine the Existing EtherChannel Configuration

I use commands `show etherchannel summary` ,`show interface trunking` `show spanning-tree` ,  `show ip interface brief` ,  `show cdp neighbor`to find out the following information :

On DSW1:  

- The EtherChannel ports are F0/2 to F0/8 in the channel group 1 . The state of these ports is P (bundled in port channel) and the state of port channel is SU (layer2 in use).
- The states of f0/1 to f0/8 , g0/1 to g0/2 , as well as  Port-channel 1 are up .
- The Trunking interfaces are f0/1,g0/1,g0/2 and port-channel1.
- The port f0/1 to f0/8 connect to ASW1

On ASW1 :

-  The EtherChannel ports are F0/1 to F0/8 in the channel group 1 . The state of F0/2 to F0/8 are P (bundled in port channel) and the state of port channel is SU (layer2 in use ) , but the F0/1 is Pd . 
- The states of f0/1 to f0/8 , f0/11 , as well as  Port-channel 1 are up .
- The Trunking interface is only port-channel 1. 

So , as a result , the output indicates that eight ports are bundled in Port-Channel 1 on ASW1. The port group on DSW1 contained only seven ports. The FastEthernet 0/1 port is bundled in Port-Channel 1 on ASW1 but is not bundled in Port-Channel 1 on DSW1. The (Pd) beside Fa0/1 in the output indicates that FastEthernet 0/1 is bundled in Port-Channel 1 (P d) and is the default port (Pd ).

## Step2:  Fix and Verify the EtherChannel Configuration

`DSW1(config)interface range f 0/1 - 8`
`DSW1(config-if-range)shutdown
`DSW1(config-if-range)channel-group 1 mode on 
`DSW1(config-if-range)no shutdown
