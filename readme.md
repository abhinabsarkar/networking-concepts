# Networking Concepts

1. [OSI Model](/concepts/osi-readme.md)
2. [TCP/IP addressing and subnetting basics](/concepts/subnetting-readme.md)

# Scenarios in Azure Networking

## Route network traffic with a route table
Refer this article - https://docs.microsoft.com/en-us/azure/virtual-network/tutorial-create-route-table-portal

**Requirement - All the network traffic between the three virtual networks listed below should be routed through vnet1**
* vnet1 - 20.0.0.0/16 subnet1 20.0.0.0/24 vm1 private ip 20.0.0.4
* vnet2 - 20.1.0.0/16 subnet2 20.1.0.0/24 vm2 private ip 20.1.0.4
* vnet3 - 20.2.0.0/16 subnet3 20.2.0.0/24 vm3 private ip 20.2.0.4

**Solution:**

Create peering between vnet1 & vnet2, vnet1 & vnet3
* vnet1 v1-v2 (allow forwarding to vnet2)
* vnet1 v1-v3 (allow forwarding to vnet3)

Create VM as Network Virtual Appliance (NVA)
* vm1 (20.0.0.4) in vnet1 as NVA
* Enable IP forwarding at NIC (in Azure)
* Enable IP forwarding at OS (in the VM)
 
Create Route table for vnet2 - route-table-vnet2	
* route-to-vnet3 (vnet3-address-space(target - 20.2.0.0/16), next-hop-address(nva-vnet1-ip - 20.0.0.4))	
* Associate route table to subnet2 (20.1.0.0/24)

Create Route table for vnet3 - route-table-vnet3	
* route-to-vnet2 (vnet2-address-space(target - 20.1.0.0/16), next-hop-address(nva-vnet1-ip - 20.0.0.4))	
* Associate route table to subnet3 (20.2.0.0/24)