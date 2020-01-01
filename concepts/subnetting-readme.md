# TCP/IP addressing and subnetting basics

When you configure the TCP/IP protocol on a computer, an IP address, subnet mask, and usually a default gateway are required in the TCP/IP configuration settings.

```cmd
C:\Abhinab>ipconfig
Wireless LAN adapter Wi-Fi:
   Connection-specific DNS Suffix  . : home
   IPv4 Address. . . . . . . . . . . : 192.168.2.14
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.2.1
```
TCP/IP are addressed and divided into networks and subnetworks. These networks are arbitrarily defined into three main classes (along with a few others) that have predefined sizes, each of which can be divided into smaller subnetworks.

**IP address** - An IP address is a 32-bit number that uniquely identifies a host on a TCP/IP network.  
In the above example, the address space of home network is  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;192.168.2.0/24  
where  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;192.168.2.14 is IPv4 address of the **host computer**  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;192.168.2.0 is the **Network ID** (unique identifier of the network)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0.0.0.14 is the **host ID** (identifier of the host in the Network ID)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;/24 is the **CIDR** (Classless inter-domain routing - identifies the bits reserved for the Network ID)  

**Subnet Mask** - A Subnet mask is a 32-bit string that masks an IP address, and divides the IP address into network address and host address. Subnet Mask is made by setting network bits to all "1"s and setting host bits to all "0"s.

| CIDR  |           Subnet mask in Bits             | Subnet mask in integer  |
| :----:|:-----------------------------------------:| :----------------------:|
|   /8  |   11111111.00000000.00000000.00000000     |    255.0.0.0            |
|   /5  |   11111000.00000000.00000000.00000000     |    248.0.0.0            |
|   /16 |   11111111.11111111.00000000.00000000     |    255.255.0.0          |
|   /20 |   11111111.11111111.11110000.00000000     |    255.255.240.0        |

The logical division of the network helps improve network performance and improve security.

Lining up the IP address and the subnet mask together, the network and host portions of the address can be separated:
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;11000000.10101000.00000010.00001110 -- IP address (192.168.2.14)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;11111111.11111111.11111111.00000000 -- Subnet mask (255.255.255.0)
 
The first 24 bits (the number of ones in the subnet mask) are identified as the network address, with the last 8 bits (the number of remaining zeros in the subnet mask) identified as the host address. This gives you the following:
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;11000000.10101000.01111011.00000000 -- Network address (192.168.2.0)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;00000000.00000000.00000000.00001110 -- Host address (000.000.000.14)

When a packet arrives on the 192.168.2.0 subnet (from the local subnet or a remote network), and it has a destination address of 192.168.2.14, your computer will receive it from the network and process it.

## Network classes
IP addresses are divided into classes. The most common of these are classes A, B, and C. Classes D and E exist, but are not generally used by end users. Each of the address classes has a different default subnet mask. You can identify the class of an IP address by looking at its first octet. Following are the ranges of Class A, B, and C Internet addresses, each with an example address:
 
* **Class A** networks use a default subnet mask of 255.0.0.0 and have 0-127 as their first octet. The address 10.52.36.11 is a class A address. Its first octet is 10, which is between 1 and 126, inclusive.
* **Class B** networks use a default subnet mask of 255.255.0.0 and have 128-191 as their first octet. The address 172.16.52.63 is a class B address. Its first octet is 172, which is between 128 and 191, inclusive.
* **Class C**  networks use a default subnet mask of 255.255.255.0 and have 192-223 as their first octet. The address 192.168.123.132 is a class C address. Its first octet is 192, which is between 192 and 223, inclusive.

In some scenarios, the default subnet mask values do not fit the needs of the organization, because of the physical topology of the network, or because the numbers of networks (or hosts) do not fit within the default subnet mask restrictions.

## Subnetting
A Class A, B, or C TCP/IP network can be further divided, or subnetted. It allows large networks to be divided into smaller networks, each with its own set of IP addresses. 

For example, 
* you have a wide area network with 150 hosts on three networks (in different cities) that are connected by a TCP/IP router. 
* Each of these three networks has 50 hosts. 
* You are allocated the class C network 192.168.2.0. 

This means that you can use the addresses 192.168.2.1 to 192.168.2.254 for your 150 hosts.

> Two addresses that cannot be used in your example are 192.168.2.0 and 192.168.2.255 because binary addresses with a host portion of all ones and all zeros are invalid. The zero address is invalid because it is used to specify a network without specifying a host. The 255 address (in binary notation, a host address of all ones) is used to broadcast a message to every host on a network

In this case, if you divide your network into four subnets by using a subnet mask that makes the network address larger and the possible range of host addresses smaller. For e.g., the subnet mask 255.255.255.192 (1111111.11111111.1111111.11000000) gives you four networks of 62 hosts each. In these four networks, the last 6 binary digits can be used for host addresses.

Using a subnet mask of 255.255.255.192, your 192.168.2.0 network then becomes the four networks 192.168.2.0, 192.168.2.64, 192.168.2.128 and 192.168.2.192. These four networks would have as valid host addresses:
   * 192.168.2.1-62
   * 192.168.2.65-126
   * 192.168.2.129-190
   * 192.168.2.193-254

You can see how this works by looking at two host addresses, 192.168.2.71 and 192.168.2.133. If you used the default Class C subnet mask of 255.255.255.0, both addresses are on the 192.168.2.0 network. However, if you use the subnet mask of 255.255.255.192, they are on different networks; 192.168.2.71 is on the 192.168.2.64 network, 192.168.2.133 is on the 192.168.2.128 network.

## Default gateways
If a TCP/IP computer needs to communicate with a host on another network, it will usually communicate through a device called a router. In TCP/IP terms, a router that is specified on a host, which links the host's subnet to other networks, is called a default gateway. 

When a host attempts to communicate with another device using TCP/IP, it performs a comparison process using the defined subnet mask and the destination IP address versus the subnet mask and its own IP address. The result of this comparison tells the computer whether the destination is a local host or a remote host. This is explained beautifully by Sunny in these videos here - https://www.youtube.com/watch?v=yLeuGOOrUvo & https://www.youtube.com/watch?v=Xb1JA5CIssI

If the result of this process determines the destination to be a local host, then the computer will simply send the packet on the local subnet. If the result of the comparison determines the destination to be a remote host, then the computer will forward the packet to the default gateway defined in its TCP/IP properties. It is then the responsibility of the router to forward the packet to the correct subnet.

## IP Address calculator 
For a given IP Address space, say 131.107.2.0/24
```cmd
Address:   131.107.2.0           10000011.01101011.00000010 .00000000
Netmask:   255.255.255.0 = 24    11111111.11111111.11111111 .00000000
Wildcard:  0.0.0.255             00000000.00000000.00000000 .11111111
=>
Network:   131.107.2.0/24        10000011.01101011.00000010 .00000000 (Class B)
Broadcast: 131.107.2.255         10000011.01101011.00000010 .11111111
HostMin:   131.107.2.1           10000011.01101011.00000010 .00000001
HostMax:   131.107.2.254         10000011.01101011.00000010 .11111110
Hosts/Net: 254  
```

## Glossary
* Broadcast address -- An IP address with a host portion that is all ones.
* Host -- A computer or other device on a TCP/IP network.
* Internet -- The global collection of networks that are connected together and share a common range of IP addresses.
* InterNIC -- The organization responsible for administration of IP addresses on the Internet.
* IP -- The network protocol used for sending network packets over a TCP/IP network or the Internet.
* IP Address -- A unique 32-bit address for a host on a TCP/IP network or internetwork.
* Network -- There are two uses of the term network in this article. One is a group of computers on a single physical network segment; the other is an IP network address range that is allocated by a system administrator.
* Network address -- An IP address with a host portion that is all zeros.
* Octet -- An 8-bit number, 4 of which comprise a 32-bit IP address. They have a range of 00000000-11111111 that correspond to the decimal values 0- 255.
* Packet -- A unit of data passed over a TCP/IP network or wide area network.
* Router -- A device that passes network traffic between different IP networks.
* Subnet Mask -- A 32-bit number used to distinguish the network and host portions of an IP address.
* Subnet or Subnetwork -- A smaller network created by dividing a larger network into equal parts.
* TCP/IP -- Used broadly, the set of protocols, standards and utilities commonly used on the Internet and large networks.
* Wide area network (WAN) -- A large network that is a collection of smaller networks separated by routers. The Internet is an example of a very large WAN.