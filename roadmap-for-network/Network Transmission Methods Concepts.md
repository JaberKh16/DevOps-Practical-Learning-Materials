
## a. OSI Model
- Stands for `Open Systems Interconnection (OSI) model` is a conceptual framework that standardizes the functions of a telecommunication or computing system into seven abstract layers. 
- This model helps vendors and developers create interoperable network devices and software. Below we see the seven layers of the OSI Model.

## Layers Of OSI Model

#### Physical Layer (Layer 1)

- Is the first and lowest layer of the OSI model. 
- Responsible for transmitting raw bitstreams over a physical medium. 
- This layer deals with the physical connection between devices where hardware components like-
	1. Ethernet cables, 
	2. Hubs, 
	3. Modem, 
	4. Wireless Access Point 
	5. Repeaters.
- Protocols used here are:
	1. DSL(Digital Subscriber Line)
	2. Ethernet(IEEE 802.3)
	3. Token Ring

#### Data Link Layer (Layer 2)

- Provides node-to-node data transfer - a direct link between two physically connected nodes. 
- It ensures that data frames are transmitted with proper synchronization, error detection, and correction. 
- Devices such as switches and bridges operate at this layer, using [MAC (Media Access Control)](https://en.wikipedia.org/wiki/MAC_address) addresses to identify network devices.
- Protocols used in this layer are:
	1. Ethernet
	2. Frame Relay
	3. ATM(Asynchronous Transfer Mode)
	4. HDLC(High Level Data Link Control)
	5. PPP,FDDI
	6. SDLC(Synchronous Transfer Mode)
- Responsible for -
	- Node-to-Node Data Delivery
	- Flow Control - control of amount bytes MTUs each node can transfer
	- Error Control (via Parity Check, Cyclic Redundancy Check)
	- Physical Addressing - Src MAC to Destination MAC
	- Framing
#### Network Layer (Layer 3)

- Handles packet forwarding, including the routing of packets through different routers to reach the destination network. 
- It is responsible for logical addressing and path determination, ensuring that data reaches the correct destination across multiple networks. 
- Device like- Routers operate at this layer, using [IP (Internet Protocol) addresses](https://usa.kaspersky.com/resource-center/definitions/what-is-an-ip-address?srsltid=AfmBOoq0TltVlJi8PKDn6j4yNB0V5Av5Y4srTxb32Bbbg4TcAfZ5FG8H) to identify devices and determine the most efficient path for data transmission.
- Responsible for -
	1. Host-to-Host Delivery
		- it takes the segments from the transport layer and deliver each segments as a
		 packet to the destinated host device.
	2. Logical Addressing - process of assigning src and destination ip address to data segments.
	3. Routing - process of finding the best path from src ip to destination ip over LAN's
	4. Fragmentation - process of packet fragmenting for data link layer.
- protocols used are:
	1. IP(Internet Protocol) -IP Address
	2. IPSec(Internet Protocol Security) - where encryption is used secure the ip tunneling(routing)
	3. ICMP(Internet Control Message Protocol) - used for network diagnostic
#### Transport Layer (Layer 4)

- Provides end-to-end communication services for applications. 
- Responsible for the reliable (or unreliable) delivery of data, segmentation, reassembly of messages, flow control, and error checking. 
- Protocols like `TCP (Transmission Control Protocol)` and `UDP (User Datagram Protocol)` function at this layer. 
	- TCP offers reliable, connection-oriented transmission with error recovery,
	- UDP provides faster, connectionless communication without guaranteed delivery.
	- QUIC - Quick UDP Internet Connection
		- Fixes TCP HOL(Head Of Line) Blocking
		- Integrated TLS
		- Works on HTTP3

#### Session Layer (Layer 5)

- Manages sessions between applications. 
- It establishes, maintains, and terminates connections, allowing devices to hold ongoing communications known as sessions. 
- This layer is essential for session checkpointing and recovery - basically ensuring that data transfer can resume seamlessly after interruptions. 
- Protocols and `APIs (Application Programming Interfaces)` operating at this layer coordinate communication between systems and applications like - Authentication, Authorization.

#### Presentation Layer (Layer 6)

 -  Acts as a translator between the application layer and the network format. 
 - It handles data representation, ensuring that information sent by the application layer of one system is readable by the application layer of another. 
 -  Includes data encryption and decryption, data compression, and converting data formats. Encryption protocols and data compression techniques operate at this layer to secure and optimize data transmission.

#### Application Layer (Layer 7)

- Is the topmost layer of the OSI model and provides network services directly to end-user applications. 
- It enables resource sharing, remote file access, and other network services. 
- Common protocols operating at this layer includes:
	- `HTTP/HTTPs (Hypertext Transfer Protocol)` for web browsing, 
	- `FTP (File Transfer Protocol)` for file transfers, 
	- `SMTP (Simple Mail Transfer Protocol)` for email transmission, 
	- `DNS (Domain Name System)` for resolving domain names to IP addresses.
	- `SSH(Secure Shell)`
	- `OAuth(Open Authorization)` - passwordless authentication (Google, LinkedIn etc)
	- `OIDC(Open ID Connect)`
This layer serves as the interface between the network and the application software.


![[Pasted image 20260125062241.png]]

### b. TCP/IP Model

The `Transmission Control Protocol/Internet Protocol (TCP/IP) model` is a condensed version of the `OSI` model, tailored for practical implementation on the internet and other networks. Below we see the four layers of the `TCP/IP Model`.

#### Link Layer

This layer is responsible for handling the physical aspects of network hardware and media. It includes technologies such as Ethernet for wired connections and Wi-Fi for wireless connections. The Link Layer corresponds to the Physical and Data Link Layers of the OSI model, covering everything from the physical connection to data framing.

#### Internet Layer

The `Internet Layer` manages the logical addressing of devices and the routing of packets across networks. Protocols like IP (Internet Protocol) and ICMP (Internet Control Message Protocol) operate at this layer, ensuring that data reaches its intended destination by determining logical paths for packet transmission. This layer corresponds to the Network Layer in the OSI model.

#### Transport Layer

At the `Transport Layer`, the TCP/IP model provides end-to-end communication services that are essential for the functioning of the internet. This includes the use of TCP (Transmission Control Protocol) for reliable communication and UDP (User Datagram Protocol) for faster, connectionless services. This layer ensures that data packets are delivered in a sequential and error-free manner, corresponding to the Transport Layer of the OSI model.

#### Application Layer

The `Application Layer` of the TCP/IP model contains protocols that offer specific data communication services to applications. Protocols such as HTTP (Hypertext Transfer Protocol), FTP (File Transfer Protocol), and SMTP (Simple Mail Transfer Protocol) enable functionalities like web browsing, file transfers, and email services. This layer corresponds to the top three layers of the OSI model (Session, Presentation, and Application), providing interfaces and protocols necessary for data exchange between systems.

![[Pasted image 20260125062253.png]]




#### Comparison with OSI Model:

The TCP/IP model simplifies the complex structure of the OSI model by combining certain layers for practical implementation. Specifically designed around the protocols used on the internet, the TCP/IP model is more application-oriented, focusing on the needs of real-world network communication. This design makes it more effective for internet-based data exchange, meeting modern technological needs.

![[Pasted image 20260125062341.png]]


## Protocols

`Protocols` are standardized rules that determine the formatting and processing of data to facilitate communication between devices in a network. These protocols operate at different layers within network models, each tailored to handle specific types of data and communication needs. Here’s a look at some common network protocols and their roles in data exchange.

#### Common Network Protocols

Network protocols are essential for defining how data is exchanged across networks. Each protocol operates at a specific layer of the OSI model, ensuring structured and efficient data handling.

|**Protocol**|**Description**|
|---|---|
|`HTTP (Hypertext Transfer Protocol)`|Primarily used for transferring web pages. It operates at the Application Layer, allowing browsers and servers to communicate in the delivery of web content.|
|`FTP (File Transfer Protocol)`|Facilitates the transfer of files between systems, also functioning at the Application Layer. It provides a way for users to upload or download files to and from servers.|
|`SMTP (Simple Mail Transfer Protocol)`|Handles the transmission of email. Operating at the Application Layer, it is responsible for sending messages from one server to another, ensuring they reach their intended recipients.|
|`TCP (Transmission Control Protocol)`|Ensures reliable data transmission through error checking and recovery, operating at the Transport Layer. It establishes a connection between sender and receiver to guarantee the delivery of data in the correct order.|
|`UDP (User Datagram Protocol)`|Allows for fast, connectionless communication, which operates without error recovery. This makes it ideal for applications that require speed over reliability, such as streaming services. UDP operates at the Transport Layer.|
|`IP (Internet Protocol)`|Crucial for routing packets across network boundaries, functioning at the Internet Layer. It handles the addressing and routing of packets to ensure they travel from the source to the destination across diverse networks.|

---

## Transmission

`Transmission` in networking refers to the process of sending data signals over a medium from one device to another. To further understand this concept, let’s examine the different types of transmission, the modes in which these transmissions can occur, and the media that carry the signals.

#### Transmission Types

Transmission in networking can be categorized into two main types: `analog` and `digital`. Analog transmission uses continuous signals to represent information, commonly seen in traditional radio broadcasts. In contrast, digital transmission employs discrete signals (bits) to encode data, which is typical in modern communication technologies like computer networks and digital telephony.

#### Transmission Modes

Transmission modes define how data is sent between two devices. `Simplex` mode allows one-way communication only, such as from a keyboard to a computer, where signals travel in a single direction. `Half-duplex` mode permits two-way communication but not simultaneously; examples include walkie-talkies where users must take turns speaking. `Full-duplex` mode, used in telephone calls, supports two-way communication simultaneously, allowing both parties to speak and listen at the same time.

#### Transmission Media

The physical means by which data is transmitted in a network is known as transmission media, which can be wired or wireless. Wired media includes `twisted pair` cables, commonly used in Ethernet networks and local area network (LAN) connections; `coaxial` cables, used for cable TV and early Ethernet; and `fiber optic` cables, which transmit data as light pulses and are essential for high-speed internet backbones. Wireless media, on the other hand, encompasses `radio waves` for Wi-Fi and cellular networks, `microwaves` for satellite communications, and `infrared` technology used for short-range communications like remote controls. Each type of media has its specific use cases depending on the requirements of the network environment.