# Network<!-- omit in toc -->

## Index<!-- omit in toc -->
- [What is an IP address](#what-is-an-ip-address)
- [What is a Netmask](#what-is-a-netmask)
- [What is the subnet of an IP with Netmask](#what-is-the-subnet-of-an-ip-with-netmask)
- [What is the broadcast address of a subnet](#what-is-the-broadcast-address-of-a-subnet)
- [What are the different way to represent an ip address with the Netmask](#what-are-the-different-way-to-represent-an-ip-address-with-the-netmask)
- [What are the difference between public and private IPs](#what-are-the-difference-between-public-and-private-ips)
- [What is a class of IP address](#what-is-a-class-of-ip-address)
- [What is TCP](#what-is-tcp)
- [What is UDP](#what-is-udp)
- [What are the network layers](#what-are-the-network-layers)
- [What is the OSI model](#what-is-the-osi-model)
- [What is a DHCP server and the DHCP protocol](#what-is-a-dhcp-server-and-the-dhcp-protocol)
- [What is a DNS server and the DNS protocol](#what-is-a-dns-server-and-the-dns-protocol)
- [What are the rules to make 2 devices communicate using IP addresses](#what-are-the-rules-to-make-2-devices-communicate-using-ip-addresses)
- [How routing is working with IP](#how-routing-is-working-with-ip)
- [What is a default gateway for routing](#what-is-a-default-gateway-for-routing)
- [What is a port from an IP point of view and what is it used for when connecting
to an other device](#what-is-a-port-from-an-ip-point-of-view-and-what-is-it-used-for-when-connecting-to-an-other-device)


## What is an IP address
An **Internet Protocol** address (IP address) is a **numerical label assigned to each device connected to a computer network** that uses the Internet Protocol for communication.

An IP address serves two main functions: host or network interface identification and location addressing.

<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What is a Netmask
A netmask is a **32-bit binary mask used to divide an IP address into subnets** and specify the network's available hosts.

In a netmask, two of the possible addresses, represented as the final byte, are always pre-assigned and unavailable for custom assignment. For example, in 255.255.225.0, "0" is the assigned network address. In 255.255.255.255, the final "255" is the assigned broadcast address. These two values cannot be used for IP address assignment.

A simple formula can be used to determine the capable **amount of networks a netmask can support**:
> 2^(netmask length - # of used segments) - 2

To determine the **number of hosts a netmask is capable of supporting**, use the following formula:
> 2^(# of zeroes) - 2

<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What is the subnet of an IP with Netmask
A subnetwork or **subnet is a logical subdivision of an IP network**. The practice of dividing a network into two or more networks is called subnetting.

For IPv4, a network may also be characterized by its subnet mask or netmask, which is the bitmask that when applied by a bitwise AND operation to any IP address in the network, yields the routing prefix. Subnet masks are also expressed in dot-decimal notation like an address. For example, 255.255.255.0 is the subnet mask for the prefix 198.51.100.0/24.
<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What is the broadcast address of a subnet
A special address that **replaces the recipient addresses** in question.

Broadcasting in a computer network is transmitting a message which does not require a response to all users of the network.One computer in a network sends a data packet to all other users at the same time. The sender does not need to indicate recipient addresses – this is how the broadcast process differs from unicast, where only a single known recipient is addressed. The general advantage of broadcasting is that information can be distributed without having to be transmitted multiple times.

<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What are the different way to represent an ip address with the Netmask


<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What are the difference between public and private IPs
A **public IP address** is the address that is assigned to a computing device **to allow direct access over the Internet**.

A **private IP address** is the address space allocated **to allow organizations to create their own private network**.

![alt text](https://github.com/Karisti/cheatsheet/blob/master/network/Screenshot_2.png)
<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What is a class of IP address
![alt text](https://github.com/Karisti/cheatsheet/blob/master/network/Screenshot_1.png)

<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What is TCP
The Transmission Control Protocol (TCP) is **one of the main protocols** of the Internet protocol suite. It originated in the initial network implementation in which **it complemented the Internet Protocol (IP)**. Therefore, the entire suite is commonly referred to as TCP/IP. TCP **provides reliable, ordered, and error-checked delivery of a stream of octets (bytes)** between applications running on hosts communicating via an IP network.

<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What is UDP
In computer networking, the User Datagram Protocol (UDP) is one of the core members of the Internet protocol suite.

UDP is suitable for purposes where error checking and correction are either not necessary or are performed in the application; UDP avoids the overhead of such processing in the protocol stack. Time-sensitive applications often use UDP because dropping packets is preferable to waiting for packets delayed due to retransmission, which may not be an option in a real-time system.

<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What are the network layers
The network layer is **responsible for packet forwarding including routing through intermediate routers**.

The network layer provides the means of transferring variable-length network packets from a source to a destination host via one or more networks. Within the service layering semantics of the OSI network architecture, the **network layer responds to service requests from the transport layer and issues service requests to the data link layer**.

**Functions of the network layer include:**
- **Connectionless communication**
- **Host addressing**
- **Message forwarding**

<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What is the OSI model
The OSI model can be seen as a universal language for computer networking. It’s based on the concept of splitting up a communication system into seven abstract layers, each one stacked upon the last.
![alt text](https://github.com/Karisti/cheatsheet/blob/master/network/Screenshot_3.png)

<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What is a DHCP server and the DHCP protocol
**A DHCP Server is a network server that automatically provides and assigns IP addresses, default gateways and other network parameters to client devices**. It **relies on the standard protocol known as Dynamic Host Configuration Protocol or DHCP to respond to broadcast queries by clients**.

A DHCP server automatically sends the required network parameters for clients to properly communicate on the network. Without it, the network administrator has to manually set up every client that joins the network, which can be cumbersome, especially in large networks. DHCP servers usually assign each client with a unique dynamic IP address, which changes when the client’s lease for that IP address has expired.

<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What is a DNS server and the DNS protocol
The Domain Name System (DNS) is a **hierarchical and decentralized naming system for computers, services, or other resources connected to the Internet or a private network**. It associates various information with domain names assigned to each of the participating entities. Most prominently, **it translates more readily memorized domain names to the numerical IP addresses** needed for locating and identifying computer services and devices with the underlying network protocols.

<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What are the rules to make 2 devices communicate using IP addresses
![alt text](https://github.com/Karisti/cheatsheet/blob/master/network/internet.jpg)

<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## How routing is working with IP
**IP Routing describes the process of determining the path for data to follow in order to navigate from one computer or server to another**. A packet of data traverses from its source router through a web of routers across many networks until it finally reaches its destination router using a routing algorithm. The **routing algorithm takes into account factors such as the size of a packet and its header to determine the most efficient route** to the destination. When a packet has reached a router, **the source and destination address of the packet are used in conjunction with a routing table** (list that contains the routes to a certain network) to determine the next hop address. **This process is repeated** for the next router using its own routing table until the packet has reached its destination. Because the data is divided into packets, each packet travels independently from each other and is treated as such. As a result, **each packet can be sent through a different route to the destination** if necessary.
![alt text](https://github.com/Karisti/cheatsheet/blob/master/network/Screenshot_5.png)

<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What is a default gateway for routing
A gateway is a **network node that serves as an access point to another network**, often involving not only a change of addressing, but also a different networking technology. More narrowly defined, a router merely forwards packets between networks with different network prefixes. The networking software stack of each computer contains a routing table that specifies which interface is used for transmission and which router on the network is responsible for forwarding to a specific set of addresses. **If none of these forwarding rules is appropriate for a given destination address, the default gateway is chosen as the router of last resort**. The default gateway can be specified by the route command to configure the node's routing table and default route.

In a home or small office environment, the default gateway is a device, such as a DSL router or cable router, that connects the local network to the Internet. It serves as the default gateway for all network devices.

Enterprise network systems may require many internal network segments. A device wishing to communicate with a host on the public Internet, for example, forwards the packet to the default gateway for its network segment. This router also has a default route configured to a device on an adjacent network, one hop closer to the public network.

<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What is a port from an IP point of view and what is it used for when connecting to an other device
In computer networking, a port is a communication endpoint. Physical as well as wireless connections are terminated at ports of hardware devices. At the software level, within an operating system, a port is a **logical construct that identifies a specific process or a type of network service**. **Ports are identified for each protocol** and address combination by 16-bit unsigned numbers, commonly known as the **port number**. The **most common protocols that use port numbers are** the Transmission Control Protocol (**TCP**) and the User Datagram Protocol (**UDP**).

**A port number is always associated with an IP address of a host and the protocol type of the communication**. It completes the destination or origination network address of a message. Specific port numbers are commonly reserved to identify specific services, so that an arriving packet can be easily forwarded to a running application. For this purpose, **the lowest numbered 1024 port numbers identify the historically most commonly used services**, and are called the **well-known port numbers**. Higher-numbered ports are available for general use by applications and are known as ephemeral ports.

When used as a service enumeration, ports provide a multiplexing service for multiple services or multiple communication sessions at one network address. In the client–server model of application architecture multiple simultaneous communication sessions may be initiated for the same service.

<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>
