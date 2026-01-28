**Date:** 2026-01-28

**Topology:** 
<img width="883" height="184" alt="image" src="https://github.com/user-attachments/assets/9adb2620-4bed-499d-a24d-a84d0f65edfb" />


## 1. Goal
1. Use the System Configuraton Dialog to configure R1 and SW1 according to the following, and save the configurations to NVRAM:
(Don't use basic management setup)
R1:
Hostname: R1
Enable secret: Cisco
Enable password: CCNA
Virtual terminal password: CCENT
SNMP network management: No
Confiture VLAN1 interface: No
GigabitEthernet0/0: 192.168.1.1 255.255.255.0


SW1:
Hostname: SW1
Enable secret: Cisco
Enable password: CCNA
Virtual terminal password: CCENT
SNMP network management: No
VLAN1 interface: 192.168.1.2 255.255.255.0

  

## Configuration

```
Router#setup 
```
<img width="936" height="502" alt="image" src="https://github.com/user-attachments/assets/d5b27f87-cfd3-47ab-abae-e94810aacb1b" />



<img width="1015" height="588" alt="image" src="https://github.com/user-attachments/assets/ef9f1898-395a-40a0-81aa-2233dbdd8ff6" />
