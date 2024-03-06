# Net_Practice

## Level 1

- IP Addressing
- IPv4 Addressing (and address)
- Subnetting
- Subnet Mask
- Network Address
- Broadcast Address
- Valid IP Ranges (0 - 255)
- CIDR Notation

## Concepts

### TCP

TCP: Transmission Control Protocol.

It is the standard that defines how to split a message in more managable packets and ensuring a reliable transmission over the internet. It is an impementation of the 'packet switching model'.

Check: Circuit-switching, vs. Message-switching, vs Packet-switching.

In the OSI (Open System Interconnection) Model, TCP resides in the Transport Layer (Layer 4).

The TCP protocol is often associated with the IP protocol and we talk of TCP/IP.

- [Packet switching](https://en.wikipedia.org/wiki/Packet_switching)
- [Circuit switching](https://en.wikipedia.org/wiki/Circuit_switching)
- [Message switching](https://en.wikipedia.org/wiki/Message_switching)

### IP

The IP protocol is responsible to route messages across a network. In association with the TCP protocol, the messages will be packets. The IP protocol ensure a fast routing through the network and it doesn't guarantee order or reliability.

The IP protocol is part of the Network Layer (Layer 3) of the OSI model.

### IPv4

IPv4 is essentially a protocol for communication over the Internet and other packet-switched networks, defining how devices on the network are identified through unique IP addresses. This identification facilitates the routing of data between devices across the network, enabling them to communicate with each other.

An **IPv4 address** is a 32-bits address. Normally is written in a human readable notation (dotted-decimal format) like 192.108.42.64 (in IPv4).

The purpose of an IP Address is to **locate** a device (a computer, a printer, a server) on a network. Devices on a network are called 'nodes', but also to **identfy**.

- [ ] Explain the difference between the two purposes.

An IP address is divided in an _network part_ and in a _host part_: the _subnet mask_ defines how many bits are the network part and many the host part. The network part defines the part of the address shared by all the devices on a network and the host part defines which defines the precise identifiers of the 'host'. An host, is a device, and it's called like that, cause it hosts an IP Address. The network part is also called 'routing prefix'.

Different internet service providers (ISP) can use different subnet masks to manage their network space.

- [ ] Think about the fact that we have access to the Internet always through to an Internet provider.

When we register to have Internet access at a ISP we get something like a modem, which will have an IP address which identifies this device in their network. This will be a private internet address, not accessible from the internet, cause we don't want people accessing our computer from the internet.

When we want to publish our website, we register to another ISP and then we get an IP which is public this time, the same if we use a service like GitHub Pages: we get a publich IP, i.e. our website is connected with a public IP.

We could also get "real" internet access, but we would request an IP address block from a RIR, the [Regiona Internet Registry](https://en.wikipedia.org/wiki/Regional_Internet_registry). Which is the authority that assigns blocks of IP addresses to the ISPs. And you need also specialized equipment and connectivity directly to an internet exchange point (IXP) or to a major network provider.

There are **private** and **public** IP addresses.

- Private IP addresses are designed for internal networks, this could be the internal network 'behind' our home router, or the internal network 'behind' our Internet Service Provider (ISP). They are not meant to be publicly accessed.
  Common private ranges are 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16.
- Public internet addresses are meant to be accessed from any other device, which has access to the internet. They are assigned by ISPs.

### Subnetting

In a subnet we have different 'reserved' addresses:

- Network Address: the address with all the host bits set to 0. If we have an

Example

IP Address (with subnet mask): 192.168.1.100/24 (255.255.255.0)

- Network address: 192.168.1.0
- Broadcast address: 192.168.1.255
- Default Gateway: 192.168.1.1 (normally) - This is the router on the network.

The standards for network addresses, broadcasts, subnet masks, and gateways are defined as part of the Internet Protocol (IP) specifications, ensuring all IP-based devices know how to operate.

- [ ] Problem about subnet masking and IP: theoretically two indentical IP could indicate two different adresses, cause their subnet mask is different. So my idea to solve this problem and route messages correctly is that or the subnet mask is alwasy travelling with the IP address or there is a layer on the 'raw' internet beyond the nodes of the IPS, in which all the IP addresses have the same subnet mask.

#### How to: subnet range from IP Address

How to find out the range of a subnet for a given IP address and a given subnet mask.

### CIDR Notation

"192.168.1.1" with subnet mask "255.255.255.0", you'd use "192.168.1.1/24".

### Nodes

- Switch
- Router
- Client

### Switch

Does nothing (for our purposes). It divides the subnet in multiple parts and it keeps the part with no devices involved in the communication free.

### Router

It is a device that connects two or more packet-switched networks or subnetworks. It forwards data packets to their intended IP addresses. To this purpose it has a **internal routing table**, which is a list of paths to various network destinations.

Normally a router becomes a packet which wants to reach a ceratin IP address (with a certain mask). The router check if any of its hosts match the address, if it's not the case, it checks if it has any rule to forward packets for certain IP adresses to a specific address (normally another connected router), if this is not the case then it send the packet to the default gateway

### Default gateway

The default gateway is a network node (usually a router), that serves as an access point or IP router that a computer in a network uses to send information to a computer outside its network or to the internet.If the router (serving as the default gateway) doesn't recognise the IP address of a message as being part of its network, or doesn't have a specific route for the destination IP address, it will forward the message to the default gateway (normally another router or the internet)

The default gateway is the default 'exit point for the local network, if the IP address is not part of that network.

Normally is used to provide a pathway for outbound traffic from a local network to reach the internet.

The information about the default gateway is stored in the routing table.

The default gateway is indicated in the destination with the IP Address of 0.0.0.0 and a subnetting mask of 0.0.0.0. So we can write it as 0.0.0.0/0. This notation matches all possible addresses, cause the subnet mask is 0.0.0.0 on a network address 0.0.0.- for address not in the network and for address for which we don't have pathways in the routing table, just send the packet to the node associated to the default gateway as next node.

https://en.wikipedia.org/wiki/Default_gateway

#### Resources

- IPv4 (wiki): https://en.wikipedia.org/wiki/Internet_Protocol_version_4#:~:text=Internet%20Protocol%20version%204%20(IPv4,the%20ARPANET%20in%20January%201983.

- Youssef Agnaou [NetPractice](https://medium.com/@imyzf/netpractice-2d2b39b6cf0a)
- [TC/IP Adressing and Subnetting - Microsoft](https://learn.microsoft.com/en-us/troubleshoot/windows-client/networking/tcpip-addressing-and-subnetting)
