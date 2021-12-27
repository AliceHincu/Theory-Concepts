credits: [radu dragos](https://www.youtube.com/watch?v=zwx5K7_ucwk&list=PLJF-bPtYvn_7rQz06fV0yxZo4Wx7uhGYu&index=19)
![image](https://user-images.githubusercontent.com/53339016/147422786-bc353c33-2d03-4918-a0db-7b5f95860040.png)

# STEP 1 - Find network details (ip addr + mask)
### 1.1 Identify networks
Our mask is 255.255.255.128 (/25). That means we have 25 digits equal to one in the binary representation, so 32-25=7 digits equal to 0. Because of that, we have 2^7 = 128 IP addresses. We have to check if we have enough IP addresses to design this network. Let's identify what local networks we have:
![image](https://user-images.githubusercontent.com/53339016/147423005-8c96acdf-9ade-406e-8afe-1c04f0463012.png)

Where: 
* N1345 has R1, R3, R4, R5. 
* N12 has R1, R2.
* N5w has R5 and Wireless.

### 1.2 Count the number of IP addresses needed
Usually: n devices (IP) + 1 router + 1NA(network address) + 1BA(broadcast address) => n+3
Particular cases: networks that interconnect routers do not need IP address for an extra router. We only need NA and BA.
* N1: 22 + 3 = 25  < **32=2^5**. We have 5 zeros, 32-5=27ones, so the mask is **/27**
* N2: 20 + 3 = 23  < **32=2^5**, so the mask is **/27**
* N3: 6 + 3 = 9    < **16=2^4**, so the mask is **/28**
* N4: 10 + 3 = 13  < **16=2^4**, so the mask is **/28**
* N5: 2 + 3 = 5    < **8=2^3**,  so the mask is **/29**
* N1345: 4 + 2 = 6 < **8=2^3**,  so the mask is **/29**
* N12: 2 + 2 = 4  <= **4=2^2**,  so the mask is **/30**
* N5w: 2 + 2 = 4  <= **4=2^2**,  so the mask is **/30**

Now we add them up. 32+32+16+16+8+8+4+4=120 < 128 

### 1.3 Split the network to give IP addresses for our devices
Recursive network split using a binary tree.
![image](https://user-images.githubusercontent.com/53339016/147425023-ed8a3cf7-d5ba-47c8-9b59-bfecfba296c5.png)

| Network name | Network address | Range of IPs | How many IPs it required | Mask | 
| -- | -- | -- | -- | -- |
| N1 | 194.95.50.0/27 | from .0  to .31 | it requires 32IPs | /27 = 255.255.255.224 |
| N2 | 194.95.50.32/27 | from .32  to .63 | it requires 32IPs | /27 = 255.255.255.224 |
| N3 | 194.95.50.64/28 | from .64  to .79 | it requires 16IPs | /28 = 255.255.255.240 |
| N4 | 194.95.50.80/28 | from .80  to .95 | it requires 16IPs | /28 = 255.255.255.240 |
| N5 | 194.95.50.96/29 | from .96  to .103 | it requires 8IPs | /29 = 255.255.255.248 |
| N6 | 194.95.50.104/29 | from .104  to .111 | it requires 8IPs | /29 = 255.255.255.248 |
| N7 | 194.95.50.112/30 | from .112  to .115 | it requires 4IPs | /30 = 255.255.255.252 |
| N8 | 194.95.50.116/30 | from .116  to .119 | it requires 4IPs | /30 = 255.255.255.252 |
| free to allocate | 194.95.50.120/29 | from .120  to .127 | it requires 8IPs | /29 = 255.255.255.248 |

Rule: Network address is the first address, the router is the second one, the server is the third one.

| Router/Server name | Network(s) it belongs to | IP from that network |
| -- | -- | -- |
| R1 | N1 | 194.95.50.1 |
| R1 | N1345 | 194.95.50.105 |
| R1 | N12 | 194.95.50.113 |
| R1 | N5w | 194.95.50.117 |
| S1 (DHCP) | N1 | 194.95.50.2 |
| R2 | N2 | 194.95.50.33 |
| R2 | N12 | 194.95.50.114 |
| S2 (Web) | N2 | 194.95.50.34 |
| R3 | N3 | 194.95.50.65 |
| R3 | N1345 | 194.95.50.106 |
| S3 (Dns) | N3 | 194.95.50.66 |
| R4 | N4 | 194.95.50.81 |
| R4 | N1345 | 194.95.50.107 |
| R5 | N5 | 194.95.50.97 |
| R5 | N1345 | 194.95.50.108 |
| Rw | N5w | 194.95.50.118 |

# STEP 2 - Packet Tracer
The difference between PT-Router and PT-Empty is that the empty one doesn't have any modules in it (hence the name Empty). We usually choose the module "PT-Router-NM-1CFE", since we have to look for "fast ethernet" ("Module provides one **Fast-Ethernet interface** for use with **copper media**. Ideal for a wide range of LAN applications, the Fast Ethernet network modules support many internetworking features and standards"). 

**How to choose the wire?** 
* **Copper straight-through**: This is a standard Ethernet cable that is used to **connect two devices that operate in different layers** of the OSI model (such as **hub to router** and **switch to PC**). It can be used with Ethernet, Fast Ethernet and Gigabit Ethernet port types.

### 2.1 Setting up the first network (N1)
We choose a pc, a PT Server, a PT Switch and a PT router. We use copper straight-through as wire. This is how it's supposed to look:
![image](https://user-images.githubusercontent.com/53339016/147502921-86f1ca30-6ab9-42db-9ad6-059147315542.png)

Now we set the IPs: 
* We start with the **router**, we go to config. We remember that the wire was used for FastEthernet 0/0, so for N1 we choose that interface and set the IP to 194.95.50.1. with mask /27.
* Before we set the **server** to become DHCP go to desktop>ip config:
   * We need to statically assign an IP: 194.95.50.2 and mask /27. 
   * To reach the Internet from the server, we pass through R1, through FastEthernet0/0, so we set the server's default gateway to 194.95.50.1.
   * We already calculated the IP of the DNS server, which is 194.95.50.66, so we set it.
* Now go back to services: DHCP 
   * We check the "On" circle, to make it a DHCP server (to set IPs for the rest of the PCs.)
   * We set the "Start IP Address:" to 194.95.50.3, because .1 is for the router and .2 is for the server.
   * We set the mask to /27 (255.255.255.224)
   * We set the "Default Gateway" to the IP of the router(194.95.50.1) 
   * We set the DNS to 194.95.50.66 (we already calculated it)
   * **PRESS SAVE**
* Now go to **PC**, Desktop > Ip Configuration, check the "DHCP" circle and check if the updated information is corect.

In the initial drawing is another PC, but I didn't add it here.
