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
| R1 | N12 | 194.95.50.114 |
| R1 | N5w | 194.95.50.117 |
| S1 (DHCP) | N1 | 194.95.50.2 |
| R2 | N2 | 194.95.50.33 |
| R2 | N12 | 194.95.50.113 |
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
We choose a pc, a PT Server, a PT Switch and a PT router. We use copper straight-through as wire. We need to add "PT-SWITCH-NM-1CFE" module for switch and "PT-ROUTER-NM-1CFE" for the router. (TIP: In the beginning, add like 4-5 modules to each device. And then copy-paste each device so you don't lose time with setting modules again and again) This is how it's supposed to look:

![image](https://user-images.githubusercontent.com/53339016/147502921-86f1ca30-6ab9-42db-9ad6-059147315542.png)

Now we set the IPs: 
* We start with the **router**, we go to config. We remember that the wire was used for FastEthernet 0/0, so for N1 we choose that interface and set the IP to 194.95.50.1. with mask /27. Set the port "On".
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

### 2.2 Setting up the second network (N2)
The beginning is the same as N1, same devices, same wire.

![image](https://user-images.githubusercontent.com/53339016/147510017-16388d7b-e55e-4304-bec0-760a92913dcc.png)

Now we set the IPs: 
* We start with the **router**, we go to config. We remember that the wire was used for FastEthernet 0/0, so for N2 we choose that interface and set the IP to 194.95.50.33 with mask /27. Set the port "On".
* Before we set the **Web server** to become HTTP go to desktop>ip config:
   * We need to statically assign an IP: 194.95.50.34 and mask /27. 
   * To reach the Internet from the server, we pass through R2, through FastEthernet0/0, so we set the server's default gateway to 194.95.50.33
   * We already calculated the IP of the DNS server, which is 194.95.50.66, so we set it.
* Now go back to services: DHCP (We can also set this one to DHCP, to make our lives easier): 
   * We check the "On" circle, to make it a DHCP server (to set IPs for the rest of the PCs.)
   * We set the "Start IP Address:" to 194.95.50.35, because .33 is for the router and .34 is for the server.
   * We set the mask to /27 (255.255.255.224)
   * We set the "Default Gateway" to the IP of the router(194.95.50.33) 
   * We set the DNS to 194.95.50.66 (we already calculated it)
   * **PRESS SAVE**
* Now go back to services: HTTP :
   * Usually it's already on
   * Edit index.html and write "New Page" (or anything you want)
   * PRESS SAVE
* Now go to **PC**: 
   * Desktop > Ip Configuration, check the "DHCP" circle and check if the updated information is corect.
   * Desktop > Web Browser, in the URL write the server IP (194.95.50.34) and press "Go". You should see index.html ("New page").

### 2.3 Setting up the third network (N3)
The beginning is the same as N1, same devices, same wire.

![image](https://user-images.githubusercontent.com/53339016/147510040-f1150f96-c519-4378-ba40-1420fe639c6a.png)


Now we set the IPs: 
* We start with the **router**, we go to config. We remember that the wire was used for FastEthernet 0/0, so for N3 we choose that interface and set the IP to 194.95.50.65 with mask /28. Set the port "On".
* Before we set the **DNS server** go to desktop>ip config:
   * We need to statically assign an IP: 194.95.50.66 and mask /28. 
   * To reach the Internet from the server, we pass through R3, through FastEthernet0/0, so we set the server's default gateway to 194.95.50.65
   * We already calculated the IP of the DNS server, which is 194.95.50.66(itself), so we set it.
* Now go back to services: DHCP (We can also set this one to DHCP, to make our lives easier): 
   * We check the "On" circle, to make it a DHCP server (to set IPs for the rest of the PCs.)
   * We set the "Start IP Address:" to 194.95.50.67, because .65 is for the router and .66 is for the server.
   * We set the mask to /28 (255.255.255.240)
   * We set the "Default Gateway" to the IP of the router(194.95.50.65) 
   * We set the DNS to 194.95.50.66 (we already calculated it)
   * **PRESS SAVE**
* This is also a **DNS** server, so it will bond a made-up name to the IP address of the Web Server. Go to Services>DNS:
   * Check the DNS Service circle to "On".
   * Put any name you want in Name (We put: "x.com")
   * Set the Address to be IP of the Web Server(194.95.50.34)
   * **PRESS ADD**
* Now go to **PC**: 
   * Desktop > Ip Configuration, check the "DHCP" circle and check if the updated information is corect.
   * Desktop > Web Browser, in the URL write the server IP (194.95.50.34) and press "Go". You should see index.html ("New page").


### 2.4 Setting up the fourth network (N4)
Here we do not have a server, so we usually have to allocate statically the PC's IP. We will do this at N5, but at N4 we will make the router DHCP(see steps below). We also have an Access Point(it's like a switch but makes the change from copper wired communication to wireless communication) and a laptop.

![image](https://user-images.githubusercontent.com/53339016/147510065-e05d11c3-81bc-41b1-9026-d09e7c887196.png)

Now we set the IPs: 
* We start with the **router**, we go to config. We remember that the wire was used for FastEthernet 0/0, so for N4 we choose that interface and set the IP to 194.95.50.81 with mask /28. Set the port "On".
* How to **make router DHCP**?
   * Go to CLI > write command "exit" until you actually exit.
   * Write "enable"
   * Write "configure t"
   * Write "ip dhcp pool x", where x is the name
   * Write "?" to see the available commands if you want
   * Write "network <IP_ADDRESS_OF_NETWORK> <MASK_OF_NETWORK>", in our case: "network 194.95.50.80 255.255.255.240"
   * Write "default-router <IP_OF_ROUTER>", in our case: "default-router 194.95.50.81"
   * Write "dns-server <IP_OF_DNS_SERVER>", in our case: "dns-server 194.95.50.66"
   * Press CTRL+Z
   * **Write "write memory" to save**
* Now go to **PC**: 
   * Desktop > Ip Configuration, check the "DHCP" circle and check if the updated information is corect.
* Now go to **Access point**:
  * Go to Config > Port 1 (which is the wireless port)  and give it a name (SSID) to the wireless network. We put the SSID to "a"(from "access point")
* Now go to **laptop**:
   *  turn off the laptop and get rid of the copper board(module) and select the wireless module "WPC300N" then turn on
   *  go to Config > Wireless0 and set the SSID to the name of the access point (SSID: "a" in our case). After a few seconds, it should connect.
   *  go to Desktop > IP Config. Set to static because if the first time the laptop connected to a random wi-fi and not to our access point, then it will have a wrong IP. So to be sure, put it on static first and then on DHCP.


### 2.5 Setting up the fifth network (N5)
Here we do not have a server, so we have to allocate statically the PC's IP.

![image](https://user-images.githubusercontent.com/53339016/147510090-40f76d4c-9202-486c-b747-3af5d937f594.png)

Now we set the IPs: 
* We start with the **router**, we go to config. We remember that the wire was used for FastEthernet 0/0, so for N5 we choose that interface and set the IP to 194.95.50.97 with mask /29. Set the port "On".
* Now go to **PC1** Desktop > Ip Configuration, check the "Static" circle and fill in the info:
   * IPv4: 194.95.50.98
   * Subnet Mask: /29  (255.255.255.248)
   * Default Gateway: 194.95.50.97
   * DNS Server: 194.95.50.66

**NOW WE BASICALLY CONFIGURED ALL OF OUR NETWORKS, BUT NOW WE HAVE TO CONFIGURE THE NETWORKS BETWEEN THEM.**

### 2.6 Connect the routers.
**Copper cross-over**: This Ethernet cable connects devices operating in the same OSI layer (such as hub to hub, PC to PC, PC to router, and PC to printer). This cable can also be used with Ethernet, Fast Ethernet and Gigabit Ethernet port types.

* Connect R1 and R2 to make N12. 
   * N12 is 194.95.50.112/30
   * R1 is 194.95.50.113 on FastEthernet1/0, with subnet Mask 255.255.255.252 and then "On"
   * R2 is 194.95.50.114 on FastEthernet1/0, with subnet Mask 255.255.255.252 and then "On"
* Connect R1, R3, R4, R5 to make N1345.
   * N1345 is 194.95.50.104/29
   * R1 is 194.95.50.105 on FastEthernet2/0, with subnet Mask 255.255.255.248 and then "On"
   * R3 is 194.95.50.106 on FastEthernet1/0, with subnet Mask 255.255.255.248 and then "On"
   * R4 is 194.95.50.107 on FastEthernet1/0, with subnet Mask 255.255.255.248 and then "On"
   * R5 is 194.95.50.108 on FastEthernet1/0, with subnet Mask 255.255.255.248 and then "On"
* Connect R5 with Wireless to create N5w.
   * N5 is 194.95.50.116/30
   * When you connect the wire from wireless to router, make sure to select INTERNET, not ethernet.
   * R5 is N5 is 194.95.50.117 on FastEthernet2/0, with subnet Mask 255.255.255.252 and then "On"
   * Wireless go to Config>Internet
      * Ip is 194.95.50.118 
      * Subnet Mask 255.255.255.252 
      * Default Gateway is 194.95.50.117 (R5)
      * DNS Server is 194.95.50.66
      * you may also go to Config > Wireless and set the SSID "r" (give whatever name you want)
* For the private network
   * Connect with straight through wire the wireless with a pc (because the wireless is also a switch for LAN). Don;t forget to put DHCP.
   * Connect a phone to wireless router:
      * go to config > wireless0 and at ssid write "r" . Then check if it has an IP.

# STEP 3: Routing tables (static)
R1 knows 3 networks: N1, N12, N1345. We have to manually introduce other networks
Go to config > static and:
* for R1:
   * To reach N2, we have to introduce its network address(194.95.50.32), the mask(255.255.255.224) and the next hop which is R2(194.95.50.113), then click add
   * To reach N3, we have to introduce its network address(194.95.50.64), the mask(255.255.255.240) and the next hop which is R3(194.95.50.106), then click add
   * To reach N4, we have to introduce its network address(194.95.50.90), the mask(255.255.255.240) and the next hop which is R4(194.95.50.107), then click add
   * To reach N5, we have to introduce its network address(194.95.50.96), the mask(255.255.255.248) and the next hop which is R5(194.95.50.108), then click add
   * To reach N5w, we have to introduce its network address(194.95.50.116), the mask(255.255.255.252) and the next hop which is R3(194.95.50.108), then click add

R2 doesn't know N1, N3, N4, N5, N5w. For any of these networks, we have to pass through R1. We will set R1 as a default gateway for R2.

Go to config > static and:
* To reach other networks, we have to introduce its network address(0.0.0.0), the mask(0.0.0.0) and the next hop which is R1(194.95.50.114), then click add

R3 doesn't know N1, N2, N4, N5, N5w. 
* To reach N1, we have to introduce its network address(194.95.50.0), the mask(255.255.255.224) and the next hop which is R1(194.95.50.105) from N1345, then click add
