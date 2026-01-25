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
 -  assigned to Network Interface Card(NIC)
 -  used to send data to the destination devices while communication

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
	each devices actual physical connection with the switch - which resolves
	the network congestion problem Hub device has.
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
	- works with IP Address(Digital Virtualize Address to indentify source 
	destination devices over the internet).
	- has two types of ports:
		1. LAN (local port)
		2. WAN(internet port)
	- has three major systems:
		1. Built-in-switch
		2. Firewall
		3. DHCP Server


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



