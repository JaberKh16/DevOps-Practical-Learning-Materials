#### Network:
- a collection of interconnected devices that can communicate - sending or receiving data and resource.
#### Network Interconnection:
	1. Node - individual devices connected to network
	2. Links - communication pathways that connect nodes(wired or wireless)
	3. Data Sharing - purpose of network is to enable data sharing

	Example: Think about a ChatRoom
		1. each person/client - Nodes
		2. ability to talk and action - communication links
		3. conversion/message - data sharing

#### Importance Of Network:
	1. Resource Sharing
	2. Communication
	3. Data Access
	4. Colloboration

#### Types Of Network
	1. LAN(Local Area Network) 
		- connect devises over a short range
		- example: school, office etc
	2. WAN(Wide Area Network)
		- spans the range in wider geographical area
		- combination of multiple LANs

#### ISP(Internet Service Provider):
-  connects LANs to WAN
-  in this setup Modem(modulator-demodulator) is used
-  acts a bridge between home network and the ISP's infrastructure

#### MAC(Media Access Control) Address:
 -  defines the physical address of a device
 -  its consists of 12 digits hexadecimal number
	 -  example: 
		 1. Windows MAC Format:  00:1A:2B:3C:4D:5E
		 2.  Linux MAC Format:         08:76:54:32:1D:AB 
		 3. MacOS MAC Format:      A0:B1:C2:D3:E4:F5
		 
	 - where this 12 digits are divided into two parts:
		 1. Manufacture's ID
		 2. Device NIC ID
	- to check the MAC:
		in windows:  $ getmac
 -  assigned to Network Interface Card(NIC)
 -  used to send data to the destination devices while communication


#### How MAC Addresses are Used in Network Communication

MAC addresses are fundamental for local communication within a local area network (LAN), as they are used to deliver data frames to the correct physical device. When a device sends data, it encapsulates the information in a frame containing the destination MAC address; network switches then use this address to forward the frame to the appropriate port. Additionally, the `Address Resolution Protocol (ARP)` plays a crucial role by mapping IP addresses to MAC addresses, allowing devices to find the MAC address associated with a known IP address within the same network. This mapping is bridging the gap between logical IP addressing and physical hardware addressing within the LAN.

Imagine two computers, Computer A (with an IP address of 192.168.1.2, which we will discuss shortly) and Computer B (192.168.1.5), connected to the same network switch. Computer A has the MAC address `00:1A:2B:3C:4D:5E`, while Computer B's MAC address is `00:1A:2B:3C:4D:5F`. When Computer A wants to send data to Computer B, it first uses the Address Resolution Protocol (ARP) to discover Computer B's MAC address associated with its IP address. After obtaining this information, Computer A sends a data frame with the destination MAC address set to `00:1A:2B:3C:4D:5F`. The switch receives this frame and forwards it to the specific port where Computer B is connected, ensuring that the data reaches the correct device. This is illustrated in the following diagram.

![[Pasted image 20260127152502.png]]

#### Network Devises
##### 1. Hub
	- a device which connects multiple devices
	- connect through ethernet cable
	- drawback:
		- whatever devices connected to it gets the data means broadcast 
		data to every devices has connection.
		- thus leads to more network traffic leads to more bandwidth loss
		- insecure: ends up being transmited data to device which is not
		intended to get the data
##### 2. Switch
	- a device which connects multiple devices
	- has a intelligence system of MAC Address table setup which ensures 
	each devices actual physical connection with the switch - 
	which resolves	the network congestion problem Hub device has.
	- drawback of Switch:
		- only facilates the data sharing among LANs

	Mac Address Table
	------------------
		- defines the which device to what port on the switch via storing 
		device MAC Address.
	
	Table:
		Port No                 MAC Addr.
		12                   00:1A:2B:3C:4D:E

	Switch Working Mechanism
	-------------------------
	- its send packets to the destination devices via comparing the MAC
	- example:
		- packet =>  src    MAC
					dest   MAC


##### 3. Router
	- connect a LAN to the Internet
	- its main work is to forwarding of data packets between networks, 
	and ultimately directing internet traffic
	- works with IP Address(Digital Virtualize Address to indentify source 
	destination devices over the internet).
	- has two types of ports:
		1. LAN (local port)
		2. WAN(internet port)
	- has three major systems:
		1. Built-in-switch
		2. Firewall
		3. DHCP Server
	- it uses routing table and protocols- OSPF(Open Shortest Path First)
	or BGP (Border Gateway Protocol) to find most efficient path for data
	to routing across internet.
	- also enhance the security via blocking unauthrozied access or
	potential threads via incorporating features like- Firewall


##### 4. Modem
	- modem connected LANs to internet
	- it a dedicated physical connection from ISP
	- connects with Router via ethernet cable(on WAN port)
	- used to transmit analog signal and also to converts to digital signal
	- modern day router comes with modem built-in.


##### 5. Wireless Access Point
	- also known as Wireless AP.
	- this are the basically the antenna's in router(Wired Routers)
		- Wired Routers are those router which has no wireless support
		thus need an external device which allows it to connect to 
		wirelessly to provide wireless connection
	- also used to increase the signal range of the routers


##### 6. Software Firewalls

 - A `software firewall` is a security application installed on individual computers or devices that monitors and controls incoming and outgoing network traffic based on predetermined security rules. 
 - Unlike hardware firewalls that protect entire networks, software firewalls (also called Host-based firewalls) provide protection at the device level, guarding against threats that may bypass the network perimeter defenses. They help prevent unauthorized access, reject incoming packets that contain suspicious or malicious data, and can be configured to restrict access to certain applications or services. For example, most operating systems include a built-in software firewall that can be set up to block incoming connections from untrusted sources, ensuring that only legitimate network traffic reaches the device.

#### Network Protocols

`Network protocols` are the set of rules and conventions that control how data is formatted, transmitted, received, and interpreted across a network. They ensure that devices from different manufacturers, and with varying configurations, can adhere to the same standard and communicate effectively. Protocols encompass a wide range of aspects such as:

- `Data Segmentation`
- `Addressing`
- `Routing`
- `Error Checking`
- `Synchronization`

Common network protocols include:

- `TCP/IP`: ubiquitous across all internet communications
    
- `HTTP/HTTPS`: The standard for Web traffic
    
- `FTP`: File transfers
    
- `SMTP`: Email transmissions


#### Cabling and Connectors

`Cabling and connectors` are the physical materials used to link devices within a network, forming the pathways through which data is transmitted. This includes the various types of cables mentioned previously, but also connectors like the RJ-45 plug, which is used to interface cables with network devices such as computers, switches, and routers. The quality and type of cabling and connectors can affect network performance, reliability, and speed. For example, in an office setting, Ethernet cables with RJ-45 connectors might connect desktop computers to network switches, enabling high-speed data transfer across the local area network.



