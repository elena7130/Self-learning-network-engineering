**Date:** 2026-01-28

**Topology:** 
<img width="977" height="533" alt="image" src="https://github.com/user-attachments/assets/cc44eba7-18e7-48b2-a3a8-31b4284b144b" />


## Goals:

1. From the CLI of SW1, find the MAC address of SW2. From the CLI of SW2, find the MAC address of SW1.
2. Why don't the MAC addresses of PC1 and PC2 appear in the MAC address tables of SW1 and SW2?
3. Ping from PC1 to PC2 to generate traffic between them. Check the MAC address tables of the switches again.
4. Enable port security on the switch interfaces connected to PCs.
5. How many MAC addresses are allowed on a port-security enabled interface by default? Explicitly configure this setting on each switch.
6. What is the default action in the event of a port-security violation? Explicitly configure this setting on each switch.
7. Manually configure the MAC address of PC1 as a secure MAC address for SW1 F0/2;Manually configure the MAC address of PC2 as a secure MAC address for SW2 F0/2
  

## Configuration:
### 1. Using `show mac address-table`on sw1 
<img width="612" height="238" alt="image" src="https://github.com/user-attachments/assets/0e00202f-03b1-4be2-b7e4-68648e54a97b" />
### 2.Answer:
End devices like PCs do not generate BPDUs; only switches participate in STP by sending and receiving BPDUs.
### 3.After `ping 192.168.1.12` , then configure `show mac address-table`on sw1 
<img width="611" height="175" alt="image" src="https://github.com/user-attachments/assets/19e9b09e-c14b-428f-bfae-cc2f280cfa49" />
* The mac address table include the addressed of PC1,PC2 and SW2
### 4.on SW1 and SW2
```
SW1(config)int f0/2
SW1(config-if)switchport mode access
SW1(config-if)switchport port-security
-------
SW2(config)int f0/2
SW2(config-if)switchport mode access
SW2(config-if)switchport port-security 
