## Goals

Analyze, locate, and fix EtherChannel problems on your network, which could be caused by misconfiguration or incorrect design

## Topology
<img width="1038" height="398" alt="image" src="https://github.com/user-attachments/assets/ad861b87-e1f1-4a26-9409-3fab4cbc1a82" />


## Trouble Ticket 1: Solving Bandwidth Issues After Switch Replacement

Due to hardware failure, CSW1 has been temporarily replaced with a non-Cisco switch until a satisfactory replacement can be delivered. Upon installation and configuration of the temporary switch, there is a noticeable decrease of network bandwidth between the core and distribution layers. You are provided authorization to the access and distribution switches, and you have been asked to determine and correct the problem.

1. Using `show cdp neighbour`to find which links connected to DSW1 and DSW2 . 
2. Using `show etherchannel summary`to observe the port channels and member interfaces . 
3. Using `show interface state`to verify the state of interface 

   Through these commands , I found these efforts on the DSW1:
1. The state of every interfaces are nomal;
2. The interface F0/9 and F0/10 on DSW1 connect to CSW1 and they are member interfaces in the port channel 11 ;
3. The port channel 11 is down state , whereas the member interfaces are in a stand-alone state . 
4. Member interfaces that are configured inconsistent with the port channel will be put in to an EtherChannel suspended state (s).In this scenario, the member interfaces are shown as stand-alone (I)
5. Failed EtherChannel negotiation can cause a port channel to be in a down state. In this scenario, CSW1 had been replaced with a non-Cisco switch. The distribution layer switches are all running PAgP, which is a Cisco-proprietary protocol. Non-Cisco switches do not support PAgP. Therefore, I try configuring all port channels connected to CSW1 with Link Aggregation Control Protocol (LACP), a standards-based EtherChannel negotiation protocol, to see if a successful negotiation will take place.
6. I use `show running-config`find that the command `channel-group 11 mode auto`on the f0/9 and f0/10 ,so I use following command to fix the EtherChannel.
    ```
    no channel-group 11 mode auto
    channel-group 11 mode active
    ```

7. As a result , the command I fixed is work and the state of port channel 11 is up , as well as interfaces f0/9 and f0/10 are in the bundled now . 

