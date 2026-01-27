**Date:** 2026-01-27

**Topology:** 

<img width="940" height="234" alt="image" src="https://github.com/user-attachments/assets/5c47d96a-4523-406d-bae7-02e24ce13206" />


## Goals :

1.Successing to connect  to each device using SSH from PC1.

## Configuration

Step1: Configure the hostnames of SW1 and R1.

```
Switch(config)hostname SW1
Router(config)hostname R1
```

Step2: Configure R1's G0/0 interface and SW1's VLAN1 interface with the indicated IP addresses.

```
SW1(confit)interface vlan 1
SW1(confit-if )no shutdown
SW1(confit-if )ip add 192.168.1.11 255.255.255.0
SW1(confit-if )exit
SW1(confit)ip default-gateway 192.168.1.1 
```
```
R1(config)interface g0/0
R1(confit-if)no shutdown
R1(confit-if)ip add 192.168.1.1 255.255.255.0
R1(confit-if)exit
```

Step3:Configure the following user account and  a DNS domain name of cisco.com on SW1 and R1 
```
SW1(confit)enable secrect ccna
SW1(confit)usename cisco secrect ccna
SW1(confit)ip domain name cisco.com

R1(confit)enable secrect ccna
R1(confit)usename cisco secrect ccna
R1(confit)ip domain name cisco.com
```

Step4: Generate the keys
```
SW1(confit)crypto key generate rsa 
# then input the number of size , for example :2048
R1(confit)crypto key generate rsa 
```

Step4: Enable SSH version 2 on each device.

```
SW1(confit)access-list 1 permit host 192.168.1.11
SW1(confit)ip ssh version 2
SW1(confit-line)line vty 0 15
SW1(confit-line)login local 
#require the use of the local user database to connect to the vty lines
SW1(confit-line)transport input ssh 
allow only SSH connections to the vty lines
SW1(confit-line)access-class 1 in
allow only PC1 connections to the vty lines
SW1(confit-line)exec-timeout 5 0 
#terminate connections after 5 minutes of inactivity
```
* On the R1 , configure same as SW1

Step4: Using PC1 connect to each device 
```
C:\>ssh -l cisco 192.168.1.1  # connect to the R1
C:\>ssh -l cisco 192.168.1.2  # connect to the SW1
```
