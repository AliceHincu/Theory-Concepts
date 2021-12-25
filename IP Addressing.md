# IP Address
**An IP address is an address used in order to uniquely identify a device on an IP network**(more in depth: we identify a network card in a computer). The address is made up of **32 binary bits**, which can be divisible into a **network portion** and **host portion** with the help of a subnet mask.

The 32 binary bits are broken into four octets (1 octet = 8 bits). Each octet is converted to decimal and separated by a period (dot). For this reason, an IP address is said to be expressed in dotted decimal format (for example, 172.16.81.100). The value in each octet ranges from 0 to 255 decimal, or 00000000 - 11111111 binary.

Dotted Decimal Notation:

![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/IP_addressing_1.jpg)

# Classful Addressing
The 32 bit IP address is divided into five sub-classes. These are:
* Class A
* Class B
* Class C
* Class D
* Class E
Each of these classes has a valid range of IP addresses. Classes D and E are reserved for multicast and experimental purposes respectively. The order of bits in the first octet determine the classes of IP address.

IPv4 address is divided into two parts:
* Network ID
* Host ID
![image](https://user-images.githubusercontent.com/53339016/147363182-baa231c7-fc5e-4e6f-8859-46e6d8e68412.png)

### Class A
IP address belonging to class A are assigned to the networks that contain a large number of hosts.
* The network ID is 8 bits long.
* The host ID is 24 bits long.

The higher order bit of the first octet in class A is always set to 0. The remaining 7 bits in first octet are used to determine network ID. The 24 bits of host ID are used to determine the host in any network. The default subnet mask for class A is 255.x.x.x. 

Therefore, class A has a total of:
* 2^7-2= **126 network ID**
  * 2^7 because from the 8bits for the network ID, the first one is 0, so only 7bits remain that can be 1 or 0
  * Here 2 address are subtracted because 0.0.0.0 and 127.x.y.z are special addresses.
* 2^24 – 2 = 16,777,214 host ID
  * We subtract to because two are reserved: the broadcast address and the network address. 
  
IP addresses belonging to class A ranges from 1.x.x.x – 126.x.x.x

### Class B
IP address belonging to class B are assigned to the networks that ranges from medium-sized to large-sized networks.
* The network ID is 16 bits long.
* The host ID is 16 bits long.

The higher order bits of the first octet of IP addresses of class B are always set to 10. The remaining 14 bits are used to determine network ID. The 16 bits of host ID is used to determine the host in any network. The default sub-net mask for class B is 255.255.x.x. 

Class B has a total of:
* 2^14 = 16384 network address
* 2^16 – 2 = 65534 host address

IP addresses belonging to class B ranges from 128.0.x.x – 191.255.x.x.

### Class C
IP address belonging to class C are assigned to small-sized networks.
* The network ID is 24 bits long.
* The host ID is 8 bits long.
The higher order bits of the first octet of IP addresses of class C are always set to 110. The remaining 21 bits are used to determine network ID. The 8 bits of host ID is used to determine the host in any network. The default sub-net mask for class C is 255.255.255.x. 

Class C has a total of:
* 2^21 = 2097152 network address
* 2^8 – 2 = 254 host address

IP addresses belonging to class C ranges from 192.0.0.x – 223.255.255.x.

### Class D
IP address belonging to class D are reserved for multi-casting. The higher order bits of the first octet of IP addresses belonging to class D are always set to 1110. The remaining bits are for the address that interested hosts recognize.

Class D does not posses any sub-net mask. IP addresses belonging to class D ranges from 224.0.0.0 – 239.255.255.255.

### Class E:
IP addresses belonging to class E are reserved for experimental and research purposes. IP addresses of class E ranges from 240.0.0.0 – 255.255.255.254. This class doesn’t have any sub-net mask. The higher order bits of first octet of class E are always set to 1111.

### Rules for assigning Host ID
Host ID’s are used to identify a host within a network. The host ID are assigned based on the following rules:
* Within any network, the host ID must be unique to that network.
* Host ID in which all bits are set to 0 cannot be assigned because this host ID is used to represent the network ID of the IP address.
* Host ID in which all bits are set to 1 cannot be assigned because this host ID is reserved as a broadcast address to send packets to all the hosts present on that particular network.

### Rules for assigning Network ID
Hosts that are located on the same physical network are identified by the network ID, as all host on the same physical network is assigned the same network ID. The network ID is assigned based on the following rules:
* The network ID cannot start with 127 because 127 belongs to class A address and is reserved for internal loop-back functions.
* All bits of network ID set to 1 are reserved for use as an IP broadcast address and therefore, cannot be used.
* All bits of network ID set to 0 are used to denote a specific host on the local network and are not routed and therefore, aren’t used.

### Problems with Classful Addressing
The problem with this classful addressing method is that millions of class A address are wasted, many of the class B address are wasted, whereas, number of addresses available in class C is so small that it cannot cater the needs of organizations. Class D addresses are used for multicast routing and are therefore available as a single block only. Class E addresses are reserved.

# CIDR (Classless Inter-Domain Routing or supernetting)
CIDR (Classless Inter-Domain Routing) -- also known as supernetting -- is a method of assigning Internet Protocol (IP) addresses that improves the efficiency of address distribution and replaces the previous system based on Class A, Class B and Class C networks. **The initial goal of CIDR was to slow the increase of routing tables on routers across the internet and decrease the rapid exhaustion of IPv4 addresses**. As a result, the number of available internet addresses has greatly increased.

An IP address is represented by a prefix, which is the IP address of the network. It is followed by a slash, followed by a number M. M: number of leftmost contiguous bits to be used for the network mask.
* Example: 144.16.192.57 / 18

### Rules
* The number of addresses in each block must be a power of 2.(4,8,16,.... IP addresses) 
* The beginning address in each block must be divisible by the number of addresses in the block.
  * Example: A block that contains 16 addresses cannot have beginning address as 193.226.40.36. because 36 % 16 is not equal to 0, but the address 193.226.40.64 is possible, because 64 % 16 = 0.

Other example:
* 209.220.186.8/255.255.255.252 (=30) => i only have 2 bits for the hosts, so from 209.220.186.8 - 209.220.186.11. And .8 is for network address and .11 is for broadcasting. 8 % 4 = 0, so it's correct

### Masks
Class A, B and C addresses have a fixed division of network and host portions and can be expressed as masks.

**Natural Masks** 
* Class A: 255.0.0.0
* Class B: 255.255.0.0
* Class C: 255.255.255.0

Masks are very flexible. Using masks, networks can be divided into smaller subnets, by extending the network portion of the address into the host portion. Advantage gained:
* We can create a large number of subnets from one network.
* Can have less number of hosts per network. (the amount of bits from the mask is reserved for the network, only the bits left are for the hosts => less number than just 255.255.255.0 for example)


### How does one get IP Addresses ?!
It gets allocated from the portion of its ISP’s address space(ISP = Internet Service Provider)

----------------------------------------------------------------------------------------------------
|  ISP's block   |   _11001000  00010111  0001_ 0000  00000000| 200.23.16.0/20 | 2^12 IPs          |
|     ---        |                  -------                   |       ---      |     ---           |
| Organization 0 |   11001000  00010111  00010000  00000000   | 200.23.16.0/23 | asking for 512IPs |
| Organization 1 |   11001000  00010111  00010010  00000000   | 200.23.18.0/23 | asking for 512IPs |
| Organization 2 |   11001000  00010111  00010100  00000000   | 200.23.20.0/23 | asking for 512IPs |
|   ...          |                   ......                   |     ...        |         .....     |
| Organization 7 |   11001000  00010111  00011110  00000000   | 200.23.30.0/23 | asking for 512IPs |

8 organizations * 512 each = 2^1 => i have used all addresses.

[Public vs Private addresses](https://help.keenetic.com/hc/en-us/articles/213965789-What-is-the-difference-between-a-public-and-private-IP-address-)

[Routing tables](https://www.geeksforgeeks.org/routing-tables-in-computer-network/)

# PROBLEMS
## pb1
Suppose we are assigned a class C network 193.226.40.0 (basically has mask /24) <br>
Divide it into three subnets:
* corresponding to three departments
* with 110, 45 and 50 hosts respectively

-------------

We know that the size of Networks in CIDR are powers of 2.
* D1(departament 1) -> 110 hosts + 1 router + network address + broadcast = 113 IPs => 128 IPs (the closest power of 2)
* D2(departament 2) -> 45 hosts + 1 router + network address + broadcast = 48 IPs   => 64 IPs
* D3(departament 3) -> 50 hosts + 1 router + network address + broadcast = 53 IPs   => 64 IPs

128 + 64 + 64 = 256 IPs needed.   
* D1 
  * 128 IPs = 2^7 and that means we need 7 bits for the hosts, so 32-7=25bits for the network so we have a mask /25
  * **193.226.40.0|25**(where 25 = 255.255.255.128) => from 193.226.40.0 to 193.226.40.127
  * 193.226.40.0 is the network address
  * 193.226.40.127 is the broadcast address
* D2 
  * 64 IPs = 2^6 and that means we need 6 bits for the hosts, so 32-6=26bits for the network so we have a mask /26
  * **193.226.40.128|26**(where 26 = 255.255.255.192) => from 193.226.40.128 to 193.226.40.191
  * 193.226.40.128 is the network address
  * 193.226.40.191 is the broadcast address
  * The beginning address in each block must be divisible by the number of addresses in the block. 128 % 64 = 0 => It is correct 

* D3
  * 64 IPs = 2^6 and that means we need 6 bits for the hosts, so 32-6=26bits for the network so we have a mask /26
  * **193.226.40.192|26**(where 26 = 255.255.255.192) => from 193.226.40.192 to 193.226.40.255
  * 193.226.40.192 is the network address
  * 193.226.40.255 is the broadcast address
  * It also respects the divisible rule. 192 % 64 = 0.

## pb2
Suppose we have a network like this:

![image](https://user-images.githubusercontent.com/53339016/147375881-b7fc4a93-3681-43a8-8393-b4b329060f4d.png)

We need to **split this network(194.254.160.0) into subnetworks**. 

--------------------------------

To find the networks we take out the routers => 3 networks from the hosts(N1, N2, N3) and 4 others.

![image](https://user-images.githubusercontent.com/53339016/147375910-f7c0e8b8-c8c4-413e-9d58-f80d84c46185.png)

**How many IPs we need for each network?**
* N1: 8 hosts + 1 router + 1 network addr + 1 broadcast addr = 11 => 16 is the smaller power
* N2: 11 hosts + 1 router + 1 network addr + 1 broadcast addr = 14 => 16 is the smaller power
* N3: 8 hosts + 1 router + 1 network addr + 1 broadcast addr = 11 => 16 is the smaller power
* N4, N5, N6, N7: 2 routers + 1 network addr + 1 broadcast addr = 4

194.254.160.0 | 25 => 128 IPs <br>
16 + 16 + 16 + 4 + 4 + 4 + 4 = 64 IPs.

Now we have to check if the problem is solvable... can I assign all the required IP subnetworks by using that 128? When we add them up together, we have 64. 64<128 => problem solvable.

**YOU SHOULD ALWAYS START WITH THE LARGEST SUBNETWORK AND GO TOWARDS TO THE SMALLEST SUBNETWORK WHEN YOU ALLOCATE**

* N1 (we need 16 ips) 
  * 16 = 2^4. from 32 bits, we subtract 4 => the network mask is 28 => **194.254.160.0/28**. 
  * from 194.254.160.0(network addr) to 194.254.160.15(broadcast)
* N2 (we need 16 ips). Same thing but we begin from .16 => **194.254.160.16/28**
  * from 194.254.160.16(network addr) to 194.254.160.31(broadcast) 
* N3 (we need 16 ips). Same thing but we begin from .32 => **194.254.160.32/28**
  * from 194.254.160.32(network addr) to 194.254.160.47(broadcast) 
* N4 (we need 4 ips).
  * 4 = 2^2. from 32 bits, we subtract 2 => the network mask is 30 => **194.254.160.48/30**
  * from 194.254.160.48(network addr) to 194.254.160.51(broadcast)
* N5 (we need 4 ips). Same thing but we begin from .52 => **194.54.160.52/30**
  * from 194.254.160.52(network addr) to 194.254.160.55(broadcast)
* N6 (we need 4 ips). Same thing but we begin from .56 => **194.54.160.56/30**
  * from 194.254.160.56(network addr) to 194.254.160.59(broadcast)
* N7 (we need 4 ips). Same thing but we begin from .60 => **194.54.160.60/30**
  * from 194.254.160.60(network addr) to 194.254.160.63(broadcast)

!!! We are left with 128-64 = 64 IPs. 64 = 2^6 => the mask is 32-6=26. So the last one, **194.254.160.64/26**, remains free.
