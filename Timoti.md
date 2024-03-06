notes on Net practice by Timoti

# Net practice

- https://learn.microsoft.com/en-us/troubleshoot/windows-client/networking/tcpip-addressing-and-subnetting

- Practical Networking: Subnetting Mastery (YouTube) https://www.youtube.com/watch?v=BWZ-MHIhqjM

- https://subnetipv4.com/
  https://github.com/lpaube/NetPractice#important-concepts
  For quick practical subnetting technique: https://www.youtube.com/watch?v=ZxAwQB8TZsM
  Ip addresses are 32bit numbers, commonly expressed as 4 uint8 divided by points
  192.168.0.1
  This under the hood is
  11000000 . 10101000 . 00000000 . 00000001
  or more accurately
  11000000101010000000000000000001
  Part of this number points to a net and part identifies the host on that net. The **subnet mask** tells you what figures are the net address and what not.
  Example:
  255.255.255.0
  is in binary
  11111111111111111111111100000000
  Every bit set to 1 is part of the net address, so if we line up the ip and the subnet mask we get
  11000000101010000000000000000001
  ||||||||||||||||||||||||XXXXXXXX
  11111111111111111111111100000000
  The first 24 bits are net address and the last 8 host address.
  If the subnet mask was 255.255.255.192 (11111111111111111111111111000000) only the last 6 bits would be the host address.

## Network classes

Class A networks use a default subnet mask of 255.0.0.0 and have 0-127 as their first octet. The address 10.52.36.11 is a class A address. Its first octet is 10, which is between 1 and 126, inclusive.

Class B networks use a default subnet mask of 255.255.0.0 and have 128-191 as their first octet. The address 172.16.52.63 is a class B address. Its first octet is 172, which is between 128 and 191, inclusive.

Class C networks use a default subnet mask of 255.255.255.0 and have 192-223 as their first octet. The address 192.168.123.132 is a class C address. Its first octet is 192, which is between 192 and 223, inclusive.

## Subnetting

Binary addresses with a host portion of all ones and all zeros are invalid. The zero address is invalid because it's used to specify a network without specifying a host. The 255 address is used to broadcast a message to every host on a network.
Given a range of IPs, a sysadmin can further divide them (subnet them) according to their needs.

## Default gateway

A router that is specified on a host, which links the host's subnet to other networks, is called a default gateway.
When a host attempts to communicate with another device using TCP/IP, it performs a comparison process using the defined subnet mask and the destination IP address versus the subnet mask and its own IP address. The result of this comparison tells the computer whether the destination is a local host or a remote host.
If the result of this process determines the destination to be a local host, then the computer will send the packet on the local subnet. If the result of the comparison determines the destination to be a remote host, then the computer will forward the packet to the default gateway defined in its TCP/IP properties. It's then the responsibility of the router to forward the packet to the correct subnet.

## The internet protocol suite

Data transfer on the Internet is governed by a standardized suite of **protocols**. They allow varied applications and services like email, the World Wide Web, instant messaging, peer-to-peer file sharing, streaming, videoconferencing, etc.
The Internet protocol suite is often called “**TCP/IP**” after its two fundamental protocols: **TCP** (Transmission Control Protocol) and **IP** (Internet Protocol). But those two are far from the only protocols involved in packet routing!

## Classless IP Addressing: CIDR

Since the subnet mask can no longer be deduced from the IP address itself, CIDR introduced a new notation to indicate the number of bits representing the subnetwork. The four-octet IPv4 address may be followed by a slash, and then the number of subnetwork bits. For example, `128.42.42.201/28` indicates that the 28 first bits of the address represent the subnetwork.
A public address is assigned to a router by an Internet Service Provider, and allows communications over the Internet. So with a public address, one can send and receive packets from anywhere on the Internet.
A private address is assigned by a router to each device connected to it. This private address allows communication within the same subnetwork, for example between devices connected to the same WiFi network. Of course, a device cannot use its private address to send or receive packets from outside its network. This private address system saves IPv4 address space since several devices may have the same private address as long as they aren’t on the same subnet.
Basically, routers can learn which nets they're attached to and they gave an IP address on each one of them. That address serves as **gateway**: in other words it is the way out of their local network for the data packets.

## Router

The router connects multiple networks together. The router has an interface for each network it connects to.
Since the router separates different networks, the range of possible IP addresses on one of its interfaces must not overlap with the range of its other interfaces. An overlap in the IP address range would imply that the interfaces are on the same network.

#### Routing Table

[![routing_table](https://github.com/lpaube/NetPractice/raw/main/img/routing_table1.png?raw=true)](https://github.com/lpaube/NetPractice/blob/main/img/routing_table1.png?raw=true)

A routing table is a data table stored in a router or a network host that lists the routes to particular network destinations. In NetPractice, the routing table consists of 2 elements:
**Destination**: The destination specifies a network address on which a host is the end target of the packets. The route of `default` or `0.0.0.0/0`, is the route that takes effect when no other route is available for an IP destination address. The default route will use the next-hop address to send the packets on their way without giving a specific destination. The default route will match any network.

**Next hop**: The next hop refers to the next closest router a packet can go through. It is the IP address of the next router on the packet's way. Every single router maintains its routing table with a next hop address.
Sho
