# 05_NetPractice
The basic to understand networking and carrying out the project are summarized below.

---

## Internet Protocol (IP) version 4
Internet Protocol version 4 (IPv4) is the fourth version of the Internet Protocol (IP).
It is one of the core protocols of standards-based Internet.
It uses a logical addressing system and performs routing, which is the forwarding of packets from a source host to the next router that is one hop closer to the intended destination host on another network.

IPv4 is a connectionless protocol, and operates on a best-effort delivery model, in that it does not guarantee delivery, nor does it assure proper sequencing or avoidance of duplicate delivery. These aspects, including data integrity, are addressed by an upper layer transport protocol, such as the Transmission Control Protocol (TCP).
IPv4 uses a 32-bit address space which provides 4,294,967,296 (232) unique addresses, but large blocks are reserved for special networking purposes.

IPv4 addresses may be represented in any notation expressing a 32-bit integer value.

### Notation of IPv4
#### Dot-decimal notation
An IPv4-adress is a 32-bit number divided into 4 "blocks", each 8 bits. They are most often written in dot-decimal notation, which consists of four octets of the address expressed individually in decimal numbers and separated by periods.

`192.168.100.1` turns into `11000000.10101000.01100100.00000001`. The min value of each "block" is `0` and the max value is `255`.

#### CIDR notation
CIDR notation is a compact representation of an IP address and its associated network mask.
CIDR notation specifies an IP address, a slash ('/') character, and a decimal number.
The decimal number is the count of consecutive leading 1-bits (from left to right) in the network mask. The number can also be thought of as the width (in bits) of the network prefix.

### First and last address of IPv4 subnet
- The first address in a subnet is used to identify the subnet itself. In this address all host bits are 0. To avoid ambiguity in representation, this address is reserved.
- The last address has all host bits set to 1. It is used as a local broadcast address for sending messages to all devices on the subnet simultaneously.

*NOTE: However, this does not mean that every address ending in `0` or `255` cannot be used as a host address:*

*For example, in the /16 subnet `192.168.0.0/255.255.0.0`, which is equivalent to the address range `192.168.0.0 – 192.168.255.255`, the broadcast address is `192.168.255.255`. One can use the following addresses for hosts, even though they end with 255: `192.168.1.255`, `192.168.2.255`, etc.*

*Also, `192.168.0.0` is the network identifier and must not be assigned to an interface, but the addresses `192.168.1.0`, `192.168.2.0`, etc., may be assigned, despite ending with `0`.*

### Private networks
Of the approximately four billion addresses defined in IPv4, about 18 million addresses in three ranges are reserved for use in private networks. Packets addresses in these ranges are not routable in the public Internet; they are ignored by all public routers. Therefore, private hosts cannot directly communicate with public networks, but require network address translation at a routing gateway for this purpose.

| Name         | CIDR block       | Adress range                    |
| :----------: | :--------------: | :-----------------------------: |
| 24-bit block | `10.0.0.0/8`     | `10.0.0.0 – 10.255.255.255`     |
| 20-bit block | `172.16.0.0/12`  | `172.16.0.0 – 172.31.255.255`   |
| 16-bit block | `192.168.0.0/16` | `192.168.0.0 – 192.168.255.255` |

Loopback (also written loop-back) is the routing of electronic signals or digital data streams back to their source without intentional processing or modification. It is primarily a means of testing the communications infrastructure. For this purpose, the following IP adresses are reserved:

| Name      | CIDR block    | Adress range                  |
| :-------: | :-----------: | :---------------------------: |
| localhost | `127.0.0.0/8` | `127.0.0.0 – 127.255.255.255` |

---

## Network Mask
The mask is used to define which range of ip-adresses are part of the same subnet.

### Mask Notation
There are 2 different ways of writing the mask:
- "Dot-decimal notation": `255.255.255.0`
- "Class Inter-Domain Routing" or "CIDR": `/24`

The same logic as for IP addresses applies to the network-mask:<br>
`255.255.255.0` turns into `11111111.11111111.11111111.00000000`<br>
Special to the mask is, after one bit was `0` there can't be any `1` bit's anymore.<br>
So the only available numbers are:

- `255 (binary: 11111111)`
- `254 (binary: 11111110)`
- `252 (binary: 11111100)`
- `248 (binary: 11111000)`
- `240 (binary: 11110000)`
- `224 (binary: 11100000)`
- `192 (binary: 11000000)`
- `128 (binary: 10000000)`
- `0 (binary: 00000000)`

In order to have the ability to send packages between two IP-addresses they either need to be part of the same network or they need to be connected by a router which is part of both subnets.

 

## IP vs Mask

The more usable ip-addresses you need in one subnet, the less subnets you will be able to create.<br>
Here is a quick reference table for help when subnetting.
| Subnet Mask     | CIDR    | Binary Notation					   | Number of subnet   | Available Addresses per subnet|
| :-------------: | :-----: | :----------------------------------: | :----------------: | :---------------------------: |
|`255.255.255.255`| 	/32	| 	11111111.11111111.11111111.11111111| 		256			| 	1|
|`255.255.255.254`| 	/31	| 	11111111.11111111.11111111.11111110| 	 	128			| 	2|
|`255.255.255.252`| 	/30	| 	11111111.11111111.11111111.11111100| 	 	64			| 	4|
|`255.255.255.248`| 	/29	| 	11111111.11111111.11111111.11111000| 	 	32			| 	8|
|`255.255.255.240`| 	/28	| 	11111111.11111111.11111111.11110000| 	 	16			| 	16|
|`255.255.255.224`| 	/27	| 	11111111.11111111.11111111.11100000| 	 	8			| 	32|
|`255.255.255.192`| 	/26	| 	11111111.11111111.11111111.11000000| 	 	4			| 	64|
|`255.255.255.128`| 	/25	|   11111111.11111111.11111111.10000000| 	 	2			| 	128|
|`255.255.255.0`  | 	/24	| 	11111111.11111111.11111111.00000000| 	 	1			| 	256|		

---
## Switches
A switch will enable you to connect more than two devices to the same network.
Its only purpose is to distribute packages to its network.

---
## Routers
As previously mentioned a router is an interface which enables communication between different networks.
A router has the ability to be part of multiple networks.

### Routing Table
The routing table is there to store all the different paths to all the networks, the device is part of.
In Net_Practice the routing table consists of two elements, the **destination** and the **next hop**.

- The **destination** consists of the network-address that you want to send a package to, combined with the CIDR of that network: `190.3.2.252/30`. If you don't want to specify a destination, you can just set it to `default` or `0.0.0.0/0`.<br>

- The **next hop** is the address of the next router that you need to send the packages to in order to reach the destination-network.<br>

---

## Network
In order to have a functioning network, **two devices need to be on the same network**, either directly or with the help of routers which are part of both networks.

### Check if two devices are in the same network
Combine the IP-address and the mask of the devices in order to get the network-adress, doing a bit-by-bit-AND-opperation:

|      | dot-decimal     | Binary Notation						|
| :--: | :-------------: | :----------------------------------: |
|  IP  | `192.168.100.1` | `11000000.10101000.11001000.00000001`|
| MASK | `255.255.255.0` | `11111111.11111111.11111111.00000000`|

If both bits are a `1` the corresponding bit of the network-address is `1`, in any other case the corresponding bit is `0`.

|           | dot-decimal     | Binary Notation						 | CIDR |
| :-------: | :-------------: | :----------------------------------: | :--: |
|  NETWORK  | `192.168.100.0` | `11000000.10101000.11001000.00000000`| /24  |

If two devices share the same network-address, they are part of the same network and communication is ensured.