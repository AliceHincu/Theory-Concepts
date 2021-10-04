# OSI Model
There are many users who use computer network and are located all over the world. To ensure national and worldwide data communication, ISO (International Organization of Standardization) developed this model. This is called a model for Open System Interconnection (OSI) and is normally called as OSI model. The OSI Model breaks down network communication into seven layers. These layers are useful for identifying network issues.

* The open systems interconnection (OSI) model is a conceptual model created by the International Organization for Standardization which enables diverse communication systems to communicate using standard protocols. In plain English, **the OSI provides a standard for different computer systems to be able to communicate with each other**. 
* **The OSI Model can be seen as a universal language for computer networking**. It’s based on the concept of splitting up a communication system into seven abstract layers, each one stacked upon the last.
* Each layer of the OSI Model handles a specific job and communicates with the layers above and below itself. 

![](https://www.cloudflare.com/img/learning/ddos/what-is-a-ddos-attack/osi-model-7-layers.svg)

# Layer 7 : The application layer
![](https://images.ctfassets.net/slt3lc6tev37/koKt5UKczRq47xJsexfBV/c1e1b2ab237063354915d16072157bac/7-application-layer.svg)

This is the only layer that directly **interacts with data from the user**. Software applications like web browsers and email clients rely on the application layer **to initiate communications**. Application layer protocols include **HTTP** as well as **SMTP** (Simple Mail Transfer Protocol is one of the protocols that enables email communications). We’ll see that certain network functions, such as the **translation of human-friendly names** for Internet end systems like www.ietf.org to a 32-bit network address, are also done with the help of a specific application-layer protocol, namely, the domain name system (**DNS**). An application-layer protocol is distributed over multiple end systems, with the application in one end system using the protocol to exchange packets of information with the application in another end system. We’ll refer to this packet of information at the application layer as a **message**.

### Functions of Application Layer
* **Identifying communication partners**: The application layer identifies the availability of communication partners for an application with data to transmit.
* **Determining resource availability**: The application layer determines whether sufficient network resources are available for the requested communication.
* **Synchronizing communication**: All the communications occur between the applications requires cooperation which is managed by an application layer.

### Services of Application Layer
* **Network Virtual terminal**: An application layer allows a user to log on to a remote host. To do so, the application creates a software emulation of a terminal at the remote host. The user's computer talks to the software terminal, which in turn, talks to the host. The remote host thinks that it is communicating with one of its own terminals, so it allows the user to log on.
* **File Transfer, Access, and Management (FTAM)**: An application allows a user to access files in a remote computer, to retrieve files from a computer and to manage files in a remote computer. FTAM defines a hierarchical virtual file in terms of file structure, file attributes and the kind of operations performed on the files and their attributes.
* **Addressing**: To obtain communication between client and server, there is a need for addressing. When a client made a request to the server, the request contains the server address and its own address. The server response to the client request, the request contains the destination address, i.e., client address. To achieve this kind of addressing, **DNS** is used.
* **Mail Services**: An application layer provides Email forwarding and storage.
* **Directory Services**: An application contains a distributed database that provides access for global information about various objects and services.
* **Authentication**: It authenticates the sender or receiver's message or both.

### Application Layer Protocols
| Abreviation | Full Name | Description |
| -- | -- | -- |
| HTTP | HyperText Transfer Protocol | The basis for the World Wide Web. When a browser wants a web page, it sends the name of the page it wants to the server using HTTP. The server then sends the page back. |
| FTP | File Transfer Protocol | Allows users to download web pages, files, and programs that are available on other services. When the user wants to download the information to their own computer, they are using FTP. |
| SMTP | Simple Mail Transfer Protocol | Most internet systems use SMTP as a method to transfer mail from one user to another. SMTP is a push protocol and is used to send the mail whereas POP (post office protocol) or IMAP (internet message access protocol) are used to retrieve those mails at the receiver’s side.  |
| DNS | Domain Name System | The Domain Name System (DNS) is the phonebook of the Internet. Humans access information online through domain names, like nytimes.com or espn.com. Web browsers interact through Internet Protocol (IP) addresses. DNS translates domain names to IP addresses so browsers can load Internet resources. |


Main idea: **the OSI model defines the application layer as only the interface responsible for communicating with host-based and user-facing applications.**

# Layer 6: The presentation layer
![](https://images.ctfassets.net/slt3lc6tev37/60dPoRIz0Es5TjDDncEp2M/7ad742131addcbe5dc6baa16a93bf189/6-presentation-layer.svg)

The primary goal of this layer is to **take care of the syntax and semantics of the information exchanged** between two communicating systems. Presentation layer takes care that the data is sent in such a way that the receiver will understand the information(data) and will be able to use the data. Languages(syntax) can be different of the two communicating systems. Under this condition presentation layer plays a role translator. In other words, layer 6 makes the data presentable for applications to consume. The presentation layer is responsible for **translation**, **encryption**, and **compression** of data.

### Functions of Presentation Layer
* **Translation**: Before being transmitted, information in the form of characters and numbers should be changed to bit streams. The presentation layer is responsible for interoperability between encoding methods as different computers use different encoding methods. It translates data between the formats the network requires and the format the computer. Basically: **Two communicating devices communicating may be using different encoding methods, so layer 6 is responsible for translating incoming data into a syntax that the application layer of the receiving device can understand**.
* **Encryption**: It carries out encryption at the transmitter and decryption at the receiver. If the devices are communicating over an encrypted connection, layer 6 is responsible for **adding the encryption on the sender’s end** as well as **decoding the encryption on the receiver's end** so that it can present the application layer with unencrypted, readable data.
* **Compression**: It carries out data compression to reduce the bandwidth of the data to be transmitted. The primary role of Data compression is to reduce the number of bits to be transmitted. It is important in transmitting multimedia such as audio, video, text etc. This helps **improve the speed and efficiency** of communication by minimizing the amount of data that will be transferred.


# Layer 5: The session layer
This is the layer responsible for opening and closing communication between the two devices. The time between when the communication is opened and closed is known as the session. The session layer ensures that the session stays open long enough to transfer all the data being exchanged, and then promptly closes the session in order to avoid wasting resources.

The session layer also synchronizes data transfer with checkpoints. For example, if a 100 megabyte file is being transferred, the session layer could set a checkpoint every 5 megabytes. In the case of a disconnect or a crash after 52 megabytes have been transferred, the session could be resumed from the last checkpoint, meaning only 50 more megabytes of data need to be transferred. Without the checkpoints, the entire transfer would have to begin again from scratch.

### Functions of Session Layer
* **Dialog Control** : This layer allows two systems to start communication with each other in half-duplex or full-duplex.
* **Token Management**: This layer prevents two parties from attempting the same critical operation at the same time.
* **Synchronization** : This layer allows a process to add checkpoints which are considered as synchronization points into stream of data. Example: If a system is sending a file of 800 pages, adding checkpoints after every 50 pages is recommended. This ensures that 50 page unit is successfully received and acknowledged. This is beneficial at the time of crash as if a crash happens at page number 110; there is no need to retransmit 1 to100 pages.

### Session Layer Protocols
| Abreviation | Full Name | Description |
| -- | -- | -- |
| ISO 8327 | OSI protocol suite session-layer protocol | In case of a connection loss this protocol may try to recover the connection. If a connection is not used for a long period, the session-layer protocol may close it and re-open it. It provides for either full duplex or half-duplex operation and provides synchronization points in the stream of exchanged messages. |
| ZIP |  Zone Information Protocol | The Zone Information Protocol (ZIP) provides applications and processes with access to zone names. A zone is a logical grouping of nodes in an AppleTalk internet, and each zone is identified by a name. A zone name is typically used to identify an affiliation between a group of nodes, such as a group of nodes belonging to a particular department within an organization. |

Main idea: **The Session layer is used to establish, maintain and synchronizes the interaction between communicating devices**.

## Layer 4: The transport layer
![](https://images.ctfassets.net/slt3lc6tev37/76JgEjycZl12c90UByKfJA/d6578bcd7b151c489e61f42227a45713/3-network-layer.svg)

Layer 4 is responsible for **end-to-end communication between the two devices**. This includes taking data from the session layer and breaking it up into chunks called **segments** before sending it to layer 3. The transport layer on the receiving device is responsible for reassembling the segments into data the session layer can consume.

The transport layer is also responsible for flow control and error control. Flow control determines an optimal speed of transmission to ensure that a sender with a fast connection doesn’t overwhelm a receiver with a slow connection. The transport layer performs error control on the receiving end by ensuring that the data received is complete, and requesting a retransmission if it isn’t.

### Services of Transport Layer
* **End-to-end delivery**: The transport layer transmits the entire message to the destination. Therefore, it ensures the end-to-end delivery of an entire message from a source to the destination.
* **Addressing**: The transport layer provides the user address which is specified as a station or port. The port variable represents a particular TS user of a specified station known as a Transport Service access point (TSAP). Each station has only one transport entity.
* **Reliable delivery**: The transport layer provides reliability services by retransmitting the lost and damaged packets. It has 4 aspects:
   * **Error control**: In reality, no transmission will be 100 percent error-free delivery. Therefore, transport layer protocols are designed to provide error-free transmission.
   * **Sequence control**: On the sending end, the transport layer is responsible for ensuring that the packets received from the upper layers can be used by the lower layers. On the receiving end, it ensures that the various segments of a transmission can be correctly reassembled.
   * **Loss control**:  The transport layer ensures that all the fragments of a transmission arrive at the destination, not some of them. On the sending end, all the fragments of transmission are given sequence numbers by a transport layer. These sequence numbers allow the receiver's transport layer to identify the missing segment.
   * **Duplication control**: The transport layer guarantees that no duplicate data arrive at the destination. Sequence numbers are used to identify the lost packets; similarly, it allows the receiver to identify and discard duplicate segments.
* **Flow control**: Flow control is used to prevent the sender from overwhelming the receiver. If the receiver is overloaded with too much data, then the receiver discards the packets and asking for the retransmission of packets. This increases network congestion and thus, reducing the system performance.
* **Multiplexing**: The transport layer uses the multiplexing to improve transmission efficiency.
   * **Upward multiplexing**: Upward multiplexing means multiple transport layer connections use the same network connection. To make more cost-effective, the transport layer sends several transmissions bound for the same destination along the same path; this is achieved through upward multiplexing.
   * **Downward multiplexing**: Downward multiplexing means one transport layer connection uses the multiple network connections. Downward multiplexing allows the transport layer to split a connection among several paths to improve the throughput. This type of multiplexing is used when networks have a low or slow capacity.

### Transport Layer Protocols: TCP vs UDP
| TCP(Transmission control protocol) | UDP(User datagram Protocol) |
| -- | -- |
| connection-oriented services | conectionless protocol |
| guaranteed delivery, flow control | no flow control, no reliability. Allows missing packets, the sender is unable to know whether a packet has been received |
| sends packets in order so they can be stiched back together easily | packets don't necessarily arrive in order |
| slow, requires more resources | faster and needs fewer resources |
| best suited for apps that need high reliability and transmission time is relatively less critical | better suited for applications that need fast, efficient transmission, such as games |

[Read more about tcp and udp](https://www.lifesize.com/en/blog/tcp-vs-udp/)


# Layer 3: The network layer
The network layer is responsible for **facilitating data transfer between two different networks**. If the two devices communicating are on the same network, then the network layer is unnecessary. The network layer breaks up segments from the transport layer into smaller units, called packets/**datagrams**, on the sender’s device, and reassembling these packets on the receiving device. The network layer also finds the best physical path for the data to reach its destination; this is known as routing. 

Layer 4 protocols (tcp or udp) passes a segment and a destination address to the network layer. **This layer provides the service of delivery**. It includes the **IP + routing protocols** that determine the routes that datagrams take between sources and destinations. The network layer translates the logical addresses into physical addresses.

### Functions of the Network Layer
* **Routing**: When a packet reaches the router's input link, the router will move the packets to the router's output link. For example, a packet from S1 to R1 must be forwarded to the next router on the path to S2.
* **Logical Addressing**: The data link layer implements the physical addressing and network layer implements the logical addressing. Logical addressing is also used to distinguish between source and destination system. The network layer adds a header to the packet which includes the logical addresses of both the sender and the receiver.
* **Internetworking**: This is the main role of the network layer that it provides the logical connection between different types of networks.
* **Fragmentation**: The fragmentation is a process of breaking the packets into the smallest individual data units that travel through different networks.

### Services of the Network Layer
* **Guaranteed delivery**: This layer provides the service which guarantees that the packet will arrive at its destination.
* **Guaranteed delivery with bounded delay**: This service guarantees that the packet will be delivered within a specified host-to-host delay bound.
* **In-Order packets**: This service ensures that the packet arrives at the destination in the order in which they are sent.
* **Guaranteed max jitter**: This service ensures that the amount of time taken between two successive transmissions at the sender is equal to the time between their receipt at the destination.
* **Security services**: The network layer provides security by using a session key between the source and destination host. The network layer in the source host encrypts the payloads of datagrams being sent to the destination host. The network layer in the destination host would then decrypt the payload. In such a way, the network layer maintains the data integrity and source authentication services.


# Layer 2: Data-link layer
This layer is the protocol layer that transfers data between nodes(host or router) on a network segment across the physical layer. The data link layer provides the functional and procedural means to transfer data between network entities and may also provide the means to detect and possibly correct errors that can occur in the physical layer.

The data link layer is very similar to the network layer, except the data link layer facilitates data transfer between two devices on the **SAME** network. The data link layer takes packets from the network layer and breaks them into smaller pieces called **frames**. Like the network layer, the data link layer is also responsible for flow control and error control in intra-network communication (The transport layer only does flow control and error control for inter-network communications).

Examples of protocols: Wi-fi, Ethernet

# Layer 1: The physical layer
This layer includes the physical equipment involved in the data transfer, such as the cables and switches. This is also the layer where the data gets converted into a bit stream, which is a string of 1s and 0s. The physical layer of both devices must also agree on a signal convention so that the 1s can be distinguished from the 0s on both devices.

# Example
For example: Mr. Cooper wants to send Ms. Palmer an email. Mr. Cooper composes his message in an email application on his laptop and then hits ‘send’. His email application **will pass his email message over to the application layer**, which will pick a protocol (SMTP) and **pass the data along to the presentation layer**. The presentation layer will then **compress the data** and then it will hit **the session layer, which will initialize the communication session**.

The data will then hit the sender’s **transportation layer where it will be segmented**, then those **segments will be broken up into packets at the network layer**, which will be **broken down even further into frames at the data link layer**. The data link layer will then **deliver those frames to the physical layer, which will convert the data into a bitstream of 1s and 0s and send it through a physical medium, such as a cable.**

Once Ms. Palmer’s computer receives the bit stream through a physical medium (such as her wifi), the data will flow through the same series of layers on her device, but in the opposite order. First the physical layer will convert the bitstream from 1s and 0s into frames that get passed to the data link layer. The data link layer will then reassemble the frames into packets for the network layer. The network layer will then make segments out of the packets for the transport layer, which will reassemble the segments into one piece of data.

The data will then flow into the receiver's session layer, which will pass the data along to the presentation layer and then end the communication session. The presentation layer will then remove the compression and pass the raw data up to the application layer. The application layer will then feed the human-readable data along to Ms. Palmer’s email software, which will allow her to read Mr. Cooper’s email on her laptop screen.


# Read more
* [The book](https://eclass.teicrete.gr/modules/document/file.php/TP326/%CE%98%CE%B5%CF%89%CF%81%CE%AF%CE%B1%20(Lectures)/Computer_Networking_A_Top-Down_Approach.pdf)
* [Osi Model](https://osi-model.com/)
* [javatpoint](https://www.javatpoint.com/osi-model)
* [a little simplfied](https://www.studytonight.com/computer-networks/complete-osi-model)
