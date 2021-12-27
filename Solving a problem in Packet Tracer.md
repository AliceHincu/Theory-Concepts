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

P.S add table with routers and servers

# STEP 2 - Packet Tracer
