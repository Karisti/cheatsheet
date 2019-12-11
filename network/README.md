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


<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What is TCP


<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What is UDP


<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What are the network layers


<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What is the OSI model


<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What is a DHCP server and the DHCP protocol


<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What is a DNS server and the DNS protocol


<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What are the rules to make 2 devices communicate using IP addresses


<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## How routing is working with IP


<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What is a default gateway for routing


<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>


## What is a port from an IP point of view and what is it used for when connecting to an other device


<div align="right">
  <small><a href="#network">⬆ Go to Index</a></small>
</div>
