# Analog modem (Layer 1)
Analog Modem is a modem used for asynchronous transmission of data.

The word "modem" stands for “modulator/demodulator,” which refers to the fact that **modems convert digital transmission signals to analog signals and vice versa**. For example, in transmission, an analog modem converts the digital signals it receives from the local computer into audible analog signals that can be carried as electrical impulses over POTS to a destination computer or network.

Modem were developed to take digital signal coming from a digital node and convert it to an analog signal (modulating the signal) to be placed on the wire. In return, it would accept an analog signal from the wire and converting it (demodulating the signal) to a digital signal that the node could understand

Modems provide for a single connection to a network

### Signal
A signal is an electromagnetic or electrical current that is used for carrying data from one system or network to another. The signal is a function that conveys information about a phenomenon.

In electronics and telecommunications, it refers to any time-varying voltage that is an electromagnetic wave which carries information. A signal can also be defined as an observable change in quality such as quantity. There are two main types of signals: Analog signal and Digital signal.

### Analog Signal 
Analog signal is a continuous signal in which one time-varying quantity represents another time-based variable. These kind of signals works with physical values and natural phenomena such as earthquake, frequency, volcano, speed of wind, weight, lighting, etc.

![](https://cdn.guru99.com/images/2/030720_0729_AnalogvsDig1.png)

### Digital Signal
A digital signal is a signal that is used to represent data as a sequence of separate values at any point in time. It can only take on one of a fixed number of values. This type of signal represents a real number within a constant range of values. Now, let’s learn some key difference between Digital and Analog signals.

![](https://cdn.guru99.com/images/2/030720_0729_AnalogvsDig2.png)

### Analog vs Digital
Analog signals are suited for audio and video transmission while Digital signals are suited for Computing and digital electronics.

# Hub (Layer 1)
![](https://upload.wikimedia.org/wikipedia/commons/d/d9/4_port_netgear_ethernet_hub.jpg)
An Ethernet hub, active hub, network hub, repeater hub, multiport repeater, or simply hub is a network hardware device for connecting multiple Ethernet devices together and making them act as a single network segment. It has multiple input/output (I/O) ports, in which a signal introduced at the input of any port appears at the output of every port except the original incoming

A layer 1 network device such as a hub transfers data but does not manage any of the traffic coming through it. Any packet entering a port is repeated to the output of every other port except for the port of entry. Specifically, each bit or symbol is repeated as it flows in. A repeater hub can therefore only receive and forward at a single speed. Dual-speed hubs internally consist of two hubs with a bridge between them. Since every packet is repeated on every other port, packet collisions affect the entire network, limiting its overall capacity.


| Analog | Digital |
| -- | -- |
| An analog signal is a continuous signal that represents physical measurements | Digital signals are time separated signals which are generated using digital modulation |
| It is denoted by sine waves | It is denoted by square waves |
| It uses a continuous range of values that help you to represent information | Digital signal uses discrete 0 and 1 to represent information |
| Temperature sensors, FM radio signals, Photocells, Light sensor, Resistive touch screen are examples of Analog signals | Computers, CDs, DVDs are some examples of Digital signal |
| The analog signal bandwidth is low | 	The digital signal bandwidth is high |
| Analog signals are deteriorated by noise throughout transmission as well as write/read cycle | Relatively a noise-immune system without deterioration during the transmission process and write/read cycle |
| Analog hardware never offers flexible implementation | Digital hardware offers flexibility in implementation |
| It is suited for audio and video transmission | It is suited for Computing and digital electronics |
| Processing can be done in real-time and consumes lesser bandwidth compared to a digital signal | It never gives a guarantee that digital signal processing can be performed in real time |
| Analog instruments usually have a scale which is cramped at lower end and gives considerable observational errors | Digital instruments never cause any kind of observational errors |
| Analog signal doesn’t offer any fixed range | Digital signal has a finite number, i.e., 0 and 1 |

[Read more about signals](https://www.guru99.com/analog-vs-digital.html)

# Switch (Layer 2)
![](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b9/2550T-PWR-Front.jpg/555px-2550T-PWR-Front.jpg)
A layer 2 switch is primarily responsible for transporting data on a physical layer and in performing error checking on each transmitted and received frame

# Wireless Access Point (Layer 2)
![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f9/Cisco_Aironet_1131AG_-_Close.jpg/330px-Cisco_Aironet_1131AG_-_Close.jpg)
In computer networking, a wireless access point (WAP), or more generally just access point (AP), is a networking hardware device that allows other Wi-Fi devices to connect to a wired network. As a standalone device, the AP may have a wired connection to a router, but, in a wireless router, it can also be an integral component of the router itself. An AP is differentiated from a hotspot which is a physical location where Wi-Fi access is available.

# Router (Layer 3)
A router is a networking device that forwards data packets between computer networks. Routers perform the traffic directing functions on the Internet. Data sent through the internet, such as a web page or email, is in the form of data packets. A packet is typically forwarded from one router to another router through the networks that constitute an internetwork (e.g. the Internet) until it reaches its destination node.

A router is connected to two or more data lines from different IP networks. When a data packet comes in on one of the lines, the router reads the network address information in the packet header to determine the ultimate destination. Then, using information in its routing table or routing policy, it directs the packet to the next network on its journey.

