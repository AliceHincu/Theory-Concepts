# A little introduction
The network layer is the third layer (from bottom) in the OSI Model. The network layer is concerned with the delivery of a packet across multiple networks. The network layer is considered the backbone of the OSI Model. It selects and manages the best logical path for data transfer between nodes. This layer contains hardware devices such as routers, bridges, firewalls, and switches, but it actually creates a logical image of the most efficient communication route and implements it with a physical medium. Network layer protocols exist in every host or router. The router examines the header fields of all the IP packets that pass through it. Internet Protocol and Netware IPX/SPX are the most common protocols associated with the network layer.

Responsibilities of Network Layer:
* **Packet forwarding/Routing of packets**: Relaying of data packets from one network segment to another by nodes in a computer network
* **Connectionless communication(IP)**: A data transmission method used in packet-switched networks in which each data unit is separately addressed and routed based on information carried by it
* **Fragmentation of data packets**: Splitting of data packets that are too large to be transmitted on the network

**Circuit Switch vs Packet Switch**
In circuit switched network, a single path is designated for transmission of all the data packets. Whereas in case of a packet-switched network, each packet may be sent through a different path to reach the destination.

In a circuit switched network, the data packets are received in order whereas in a packet switched network, the data packets may be received out of order.

The packet switching is further subdivided into Virtual circuits and Datagram.

# IPv4 Datagram Header
Size of the header is 20 to 60 bytes.

![image](https://user-images.githubusercontent.com/53339016/147393781-f850e715-9321-4fd8-9ce2-ad4e2d52cd8b.png)

| NAME | DESCRIPTION | SIZE IN BITS |
| -- | -- | -- |
| VERSION | This field defines the version of IP. Current version of IP is IPv4 and the latest version of IP is IPv6 | 4 bits |
| HLEN | This field defines the length of the datagram header in 4-byte word. Its value must be multiplied by 4 to give the length in bytes. The minimum value for this field is 5 and the maximum is 15. | 4 bits |
| Type of service | Low Delay, High Throughput, Reliability | 8 bits |
| Total Length | Length of header + Data, which has a minimum value 20 bytes and the maximum is 65,535 bytes. | 16 bits |
| Identification | Unique Packet Id for identifying the group of fragments of a single IP datagram. When a datagram is fragmented, the value in the identification field is copied into all fragments. | 16 bits |
| Flags | First bit is reserved, and it should be 0. The second bit is called “Do not fragment” bit. If this bit is “1” then machine should not fragment the datagram but if the value of this bit is 0 then the machine should fragment the datagram if only if necessary. The third bit is called as “More Fragment Bit”. If it is 1 it means that the datagram is not the last fragment but if its value is 0 it shows that this is the last or the only fragment. | 3 flags of 1 bit each |
| Fragment Offset |This is a field which shows the relative position of this fragment with respect to the whole datagram. | 13 bit |
| Time to live | Datagram’s lifetime. To avoid looping in the network, every packet is sent with some TTL value set, which tells the network how many routers (hops) this packet can cross. At each hop, its value is decremented by one and when the value reaches zero, the packet is discarded. | 8 bits |
| Protocol | Tells the Network layer at the destination host, to which Protocol this packet belongs to, i.e. the next level Protocol. For example protocol number of ICMP is 1, TCP is 6 and UDP is 1 | 8 bits |
| Header Checksum | This field is used to keep checksum value of entire header which is then used to check if the packet is received error-free. | 16 bits |
| Source IP address | IP address of the sender | 32 bits |
| Destination IP address | IP address of the receiver | 32 bits |
| Option | Optional information such as source route, record route. Used by the Network administrator to check whether a path is working or not | - |

Due to the presence of options, the size of the datagram header can be of variable length (20 bytes to 60 bytes).

## IP Checksum
![image](https://user-images.githubusercontent.com/53339016/147394083-520b5ea0-cf45-41fd-98e5-54c1ecf3bcc1.png)

## Fragmentation
![image](https://user-images.githubusercontent.com/53339016/147394074-a9c5a99b-2fe1-4cd0-84d6-5c5a5849403b.png)

## ARP: from IP to Mac
ARP lets devices on the network ask each other which MAC addresses they have.

To find out what MAC address the router has got the computer will first put its DNS query on hold in a queue. Then it will create an ARP request. The ARP request contains a simple question. In this case, the computer wants to find out which MAC address that the 192.168.1.1 device has got. So the request is basically as follows:

“Device with IP address 192.168.1.1, reply back with your MAC address”

ARP requests are always sent as broadcasts because we don’t know what MAC address we want to send the message to. Since it is a broadcasted message, every other device on the LAN will receive the message. This is because the integrated switch in the Home Router handles the message as a broadcast and forwards it to all other ports including the integrated router. But all devices except one will notice when they read the contents of the ARP request that the message is intended for another device with IP address 192.168.1.1

The home router, which is configured with IP address 192.168.1.1, will read the message and will notice that the message is directed at itself. It will then construct an ARP reply:

“I have IP address 192.168.1.1 and my MAC address is 00:13:fe:19:c7:9e”

Every time a computer receives an ARP reply it will save the response for at least a few minutes in an ARP table (or ARP cache) in memory. This is so that the computer doesn’t have to do an ARP request for each packet it wants to send. From now on and for as long as it keeps communicating with the router it will remember the router’s MAC address. If however they stop communicating for a while then the computer will clear out the router’s MAC address from its ARP table.

Each time a computer is sending a packet to an IP address it will look in its ARP cache to see if it already knows what MAC address that is associated with that IP address.
* If the address exists in the ARP cache then the MAC address in the table will be used.
* If the address does not exist in the ARP cache, then an ARP request must be created and sent out.

## NAT - Network Address Translation
![image](https://user-images.githubusercontent.com/53339016/147395145-dbdb8bc2-3b72-44b0-9818-335568798839.png)

**Motivation**: local network uses just one IP address as far as the outside word is concerned:
* no need to allocate a range of addresses from ISP: just one IP address is used for all devices for WAN
* can change addresses of devices in local network without notifying and impacting outside world
* can change ISP without changing addresses of devices in local network
* devices inside LAN not explicitly addressable and visible by outside world (a security plus). "If they don't initiate a dialogue with the internet, the internet cannot initiate a dialogue with them - an extra layer of security, no brute force attack , no exploit buffer overflow etc"

**Limitations**:
* 16-bit port-number field: 60,000 simultaneous connections with a single LAN-side address!
* NAT is controversial:
   * routers should only process up to layer 3 (up to network layer): The original theory is that a router should not look up into the content of the data that it's transmitted (ip, tcp, udp) upward in layer 3 (which is the ip protocol), so a router should not mess with something that is above layer 3.
   * violates end-to-end argument : NAT possibility must be taken into account by app designers, e.g., P2P applications. Theoretical controversy: in practice, the ip datagram should travel unchanged between the source and the destination and this doesn't happen anymore
   * address shortage should instead be solved by IPv6
