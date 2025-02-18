# Theory

Before we begin, we need to understand three important concepts: the TCP (Transmission Control Protocol), the IP and the TCP/IP

## TCP : Transmission Control Protocol

It ensures reliable data transfer by breaking information into small packets, sending them across the network, and ensuring they arrive in the correct order at the destination.&#x20;

It also handles error correction and congestion control, thus ensuring reliable data transmission.



## IP : Internet Protocol

For this project we only use IPv4 (so i will not explain IPv6) : An IPv4-adress is a 32-bit number divided into 4 "blocks", each 8 bits. i.e.:

Every device connected to the Internet is assigned a unique IP address, which is used to identify and locate it. It is responsible for addressing and routing data packets across the network.

**An IP address is made up of two parts**:&#x20;

* one identifies the host, such as a computer or other device
* the other identifies the network to which it belongs.&#x20;

\--> TCP/IP uses a subnet mask to separate the two (corresponds to the "mask" part under each device when doing an exercise)

For example if the IP is 104.95.23.12, then the real representation in bits would be: 01101000.01011111.00010111.00001100 (the numbers can only go from 0 to 255).&#x20;

### Private Networks

* Private network IP address ranges are reserved for internal use within organizations or home/small office networks.
* The following address ranges are reserved for private networks:
  * `10.0.0.0 - 10.255.255.255`
  * `172.16.0.0 - 172.31.255.255`
  * `192.168.0.0 - 192.168.255.255`
* These ranges provide a large number of available IP addresses for private network infrastructure, allowing organizations to assign unique addresses to devices within their network without requiring public IP addresses.

### Loopback Addresses

* The loopback address range is reserved for internal testing and communication within a device.
* The loopback IP range is represented by `127.0.0.0 - 127.255.255.255.`
* The loopback address 127.0.0.1, often referred to as "localhost," is used to access the device itself. It allows network applications running on the device to communicate with each other without accessing the external network.

These reserved IP address ranges ensure that private networks can operate without conflicting with public IP addresses on the internet and provide convenient mechanisms for internal testing and communication within devices.

There is some more special ip-ranges, but for this project, you only need to remember those above.



## TCP/IP&#x20;

Together, TCP and IP provide a standardized and reliable means of transferring data between devices connected to the Internet, whether it's sending emails, browsing the web, downloading files, or streaming multimedia content.

I recommend you to watch this small video (5min) just to understand better how everything works.

{% embed url="https://www.youtube.com/watch?v=OTwp3xtd4dg" %}
TCP/IP in a nutshell
{% endembed %}

And here is a little scheme that shows how everything works:

<figure><img src="../../.gitbook/assets/image (28).png" alt="" width="371"><figcaption><p>Source: <a href="https://www.internalpointers.com/post/introduction-tcp-ip-protocol">https://www.internalpointers.com/post/introduction-tcp-ip-protocol</a></p></figcaption></figure>

##

## Masks (subnet masks)

A subnet mask, also known as subnetting mask or network mask, is a combination of bits used to divide an IP network into smaller subnets. It is used in conjunction with an IP address to determine the network address and the host address of a device on a network.

A subnet mask defines the portion of the IP address that represents the network and the portion that represents the hosts within that network.&#x20;

\--> It is often represented as a series of numbers, typically in the form of four octets separated by periods, such as `255.255.255.0.` And as for IPs, we can represent this number in bits, which would give: 11111111.11111111.11111111.00000000

Through which `255.255.255.0` is a valid mask and `255.255.128.128` is **not** a valid mask.



| CIDR |   Dot-decimal   | <p>Number of IP-addresses<br>per subnet</p> | <p>Usable IP-addresses<br>per subnet</p> | Number of subnets |
| :--: | :-------------: | :-----------------------------------------: | :--------------------------------------: | :---------------: |
|  /32 | 255.255.255.255 |                      1                      |                     0                    |        256        |
|  /31 | 255.255.255.254 |                      2                      |                     0                    |        128        |
|  /30 | 255.255.255.252 |                      4                      |                     2                    |         64        |
|  /29 | 255.255.255.248 |                      8                      |                     6                    |         32        |
|  /28 | 255.255.255.240 |                      16                     |                    14                    |         16        |
|  /27 | 255.255.255.224 |                      32                     |                    30                    |         8         |
|  /26 | 255.255.255.192 |                      64                     |                    62                    |         4         |
|  /25 | 255.255.255.128 |                     128                     |                    126                   |         2         |
|  /24 |  255.255.255.0  |                     256                     |                    254                   |         1         |

\----------------------------------------------------------------------------



## Switches

A switch is a networking device that allows you to connect multiple devices to the same network. Its main function is to receive incoming network packets and forward them to the appropriate destination device within its network.

Imagine you have a network with multiple computers, printers, and other devices. Instead of connecting each device directly to the router or modem, you can connect them to a switch. The switch acts as a central point of connection, allowing devices to communicate with each other.

When a device sends a data packet, such as a file or a request for information, the switch receives the packet and examines its destination address. Based on this information, the switch determines the appropriate port to which the packet should be forwarded. This ensures that the packet reaches the intended device and not unnecessary devices on the network.

By using a switch, you can efficiently distribute network traffic and enable communication between devices. It helps to reduce network congestion and improve overall network performance.

To see a working example, you can take a look at Level 3.





Now that you know almost all the definitions, let's take a look at a few examples to help you get the hang of it! Click on the next page :)
