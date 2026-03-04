## Date :2026-3-4
## Goal :
configure, and verify VRF-Lite.

## Topology
<img width="984" height="432" alt="image" src="https://github.com/user-attachments/assets/ee6bb73f-3e4b-4bac-bff2-6813ae107c07" />



  Before configuring VRF-Lite , I can ping f0/0 interface IP on Router Customer A through Router Main , because there is a default route to router Main from both customer routers.

  ## **Configuration - VRF-Lite**
  
```
Main(config)ip vrf CUSTOMERA
Main(config)interface f0/0
Main(config-if)ip vrf forwarding CUSTOMERA 
# When an interface is placed in a VRF instance, all IP address configuration is removed
Main(config)ip address 10.0.0.1 255.255.255.0
```

```
Main(config)ip vrf CUSTOMERB
Main(config)interface f1/0
Main(config-if)ip vrf forwarding CUSTOMERB 
Main(config)ip address 172.16.10.1 255.255.255.0
```

  ##  **Verify VRF-Lite**

After I create VRF on routers , I can't find any routing route on the global tables any more and ping IP address on Router CUSTOMER A or B directly , because now the interfaces belong to another routing table instance rather than global routing table .

So, I  should the  display the IP routing table for both VRFs :
`show ip route vrf CUSTOMERA` and `ping vrf CUSTOMERA 10.0.0.2`
