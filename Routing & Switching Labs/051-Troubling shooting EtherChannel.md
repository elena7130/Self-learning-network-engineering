**Date:** 2026-01-30

**Topology:** 
<img width="1158" height="238" alt="image" src="https://github.com/user-attachments/assets/39b7909a-e729-4496-a933-50a91480652b" />


## Goal:

The EtherChannels in the network are not functioning properly.
Troubleshoot the problems and fix them.
SW1 - SW2 = Layer 2 PAgP
SW2 - SW3 = Layer 3 Static
SW3 - SW4 = Layer 2 LACP
  
## Configuration - on SW1

  Step1-1 : I use `show etherchannel summary` to verify the  Etherchannel state and  ports . The interaces f0/1-f0/4 should be in the same group using the PAgP protocol .However, I find that the protocol was set to LACP , I applied the following configuration to fix this:
  
  ```
  SW1(config)interface range f0/1 - 4
  SW1(config-if-range)no channel-group 1
  SW1(config-if-range)no interface port-channel 1
  SW1(config-if-range)channel-group 1 mode desirable
  ```

Step1-2: I used `show interface trunk` to verify if **Port-channel 1** is operating as a trunk. The verification confirmed it is active.


## Configuration - on SW2

**Step 2-1:** Similar to Step 1, I ran `show etherchannel summary`. I found that **f0/2–f0/4** were bundled correctly, but **f0/1** was down (independent). I used `show interfaces status` and noticed the speed of **f0/1** was set to **10 Mbps**, while the other interfaces were **100 Mbps**.

**Step 2-2:** I checked **SW1** and confirmed all ports (**f0/1–f0/4**) were set to **100 Mbps**.

**Step 2-3:** On **SW2**, I entered `interface f0/1` and used the `speed 100` command to match the other members of the group.

**Step 2-4:** I checked the link between **SW2 and SW3** using `show etherchannel summary`. The interfaces **g0/1–g0/2** were not in a channel. I used the following commands to create the Layer 3 EtherChannel:
```
SW2(config)# interface range g0/1 - 2
SW2(config-if-range)# no switchport  # Change ports to Routed Mode
SW2(config-if-range)# channel-group 2 mode on
SW2(config-if-range)# exit
SW1(config)# interface port-channel 2
SW1(config-if)# no switchport
SW1(config-if)# ip address 23.0.0.1 255.255.255.252

```

## Summary:EtherChannel Troubleshooting Checklist
 
When troubleshooting EtherChannel, always verify the following parameters match on all member ports:

1. **Member Interfaces:** Ensure the correct physical ports are assigned to the correct channel group.
    
2. **Protocol:** Verify that both sides use compatible protocols (PAgP/PAgP, LACP/LACP, or On/On).
    
3. **Port Speed & Duplex:** All physical ports in a bundle **must** have the same speed and duplex settings.
    
4. **Interface Mode:** For Layer 3 EtherChannels, ensure `no switchport` is configured on both the physical interfaces and the Port-channel interface.
    
5. **VLAN/Trunking:** For Layer 2, ensure all ports belong to the same VLAN or are configured as identical trunks.
