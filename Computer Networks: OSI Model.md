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


On the short: **the OSI model defines the application layer as only the interface responsible for communicating with host-based and user-facing applications.**

## Layer 6: The presentation layer

This layer is primarily responsible for preparing data so that it can be used by the application layer; in other words, layer 6 makes the data presentable for applications to consume. The presentation layer is responsible for **translation**, **encryption**, and **compression** of data.

Two communicating devices communicating may be using different encoding methods, so layer 6 is responsible for **translating** incoming data into a syntax that the application layer of the receiving device can understand.

If the devices are communicating over an encrypted connection, layer 6 is responsible for **adding the encryption on the sender’s en**d as well as **decoding the encryption on the receiver's end** so that it can present the application layer with unencrypted, readable data.

Finally the presentation layer is also responsible for **compressing data** it receives from the application layer before delivering it to layer 5. This helps i**mprove the speed and efficiency** of communication by minimizing the amount of data that will be transferred.

![](https://images.ctfassets.net/slt3lc6tev37/60dPoRIz0Es5TjDDncEp2M/7ad742131addcbe5dc6baa16a93bf189/6-presentation-layer.svg)

## Layer 5: The session layer
This is the layer responsible for opening and closing communication between the two devices. The time between when the communication is opened and closed is known as the session. The session layer ensures that the session stays open long enough to transfer all the data being exchanged, and then promptly closes the session in order to avoid wasting resources.

The session layer also synchronizes data transfer with checkpoints. For example, if a 100 megabyte file is being transferred, the session layer could set a checkpoint every 5 megabytes. In the case of a disconnect or a crash after 52 megabytes have been transferred, the session could be resumed from the last checkpoint, meaning only 50 more megabytes of data need to be transferred. Without the checkpoints, the entire transfer would have to begin again from scratch.

## Layer 4: The transport layer
Layer 4 is responsible for **end-to-end communication between the two devices**. This includes taking data from the session layer and breaking it up into chunks called segments before sending it to layer 3. The transport layer on the receiving device is responsible for reassembling the segments into data the session layer can consume.

The transport layer is also responsible for flow control and error control. Flow control determines an optimal speed of transmission to ensure that a sender with a fast connection doesn’t overwhelm a receiver with a slow connection. The transport layer performs error control on the receiving end by ensuring that the data received is complete, and requesting a retransmission if it isn’t.

![](https://images.ctfassets.net/slt3lc6tev37/76JgEjycZl12c90UByKfJA/d6578bcd7b151c489e61f42227a45713/3-network-layer.svg)

## Layer 3: The network layer
The network layer is responsible for **facilitating data transfer between two different networks**. If the two devices communicating are on the same network, then the network layer is unnecessary. The network layer breaks up segments from the transport layer into smaller units, called packets, on the sender’s device, and reassembling these packets on the receiving device. The network layer also finds the best physical path for the data to reach its destination; this is known as routing.

## Layer 2: Data-link layer
This layer is the protocol layer that transfers data between nodes on a network segment across the physical layer.[1] The data link layer provides the functional and procedural means to transfer data between network entities and may also provide the means to detect and possibly correct errors that can occur in the physical layer.

The data link layer is very similar to the network layer, except the data link layer facilitates data transfer between two devices on the SAME network. The data link layer takes packets from the network layer and breaks them into smaller pieces called frames. Like the network layer, the data link layer is also responsible for flow control and error control in intra-network communication (The transport layer only does flow control and error control for inter-network communications).

## Layer 1: The physical layer
This layer includes the physical equipment involved in the data transfer, such as the cables and switches. This is also the layer where the data gets converted into a bit stream, which is a string of 1s and 0s. The physical layer of both devices must also agree on a signal convention so that the 1s can be distinguished from the 0s on both devices.

# Example
For example: Mr. Cooper wants to send Ms. Palmer an email. Mr. Cooper composes his message in an email application on his laptop and then hits ‘send’. His email application **will pass his email message over to the application layer**, which will pick a protocol (SMTP) and **pass the data along to the presentation layer**. The presentation layer will then **compress the data** and then it will hit **the session layer, which will initialize the communication session**.

The data will then hit the sender’s **transportation layer where it will be segmented**, then those **segments will be broken up into packets at the network layer**, which will be **broken down even further into frames at the data link layer**. The data link layer will then **deliver those frames to the physical layer, which will convert the data into a bitstream of 1s and 0s and send it through a physical medium, such as a cable.**

Once Ms. Palmer’s computer receives the bit stream through a physical medium (such as her wifi), the data will flow through the same series of layers on her device, but in the opposite order. First the physical layer will convert the bitstream from 1s and 0s into frames that get passed to the data link layer. The data link layer will then reassemble the frames into packets for the network layer. The network layer will then make segments out of the packets for the transport layer, which will reassemble the segments into one piece of data.

The data will then flow into the receiver's session layer, which will pass the data along to the presentation layer and then end the communication session. The presentation layer will then remove the compression and pass the raw data up to the application layer. The application layer will then feed the human-readable data along to Ms. Palmer’s email software, which will allow her to read Mr. Cooper’s email on her laptop screen.
