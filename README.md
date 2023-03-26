# 05_NetPractice
The basic to understand networking and caryying out the project are summarized below.

## Internet Protocol (IP) version 4
Internet Protocol version 4 (IPv4) is the fourth version of the Internet Protocol (IP).
It is one of the core protocols of standards-based internetworking methods in the Internet.
Enables internetworking at the internet layer of the Internet Protocol Suite.
It uses a logical addressing system and performs routing, which is the forwarding of packets from a source host to the next router that is one hop closer to the intended destination host on another network.

IPv4 is a connectionless protocol, and operates on a best-effort delivery model, in that it does not guarantee delivery, nor does it assure proper sequencing or avoidance of duplicate delivery. 
hese aspects, including data integrity, are addressed by an upper layer transport protocol, such as the Transmission Control Protocol (TCP).
IPv4 uses a 32-bit address space which provides 4,294,967,296 (232) unique addresses, but large blocks are reserved for special networking purposes.

IPv4 addresses may be represented in any notation expressing a 32-bit integer value.
They are most often written in dot-decimal notation, which consists of four octets of the address expressed individually in decimal numbers and separated by periods.

### Structure of IPv4
An IPv4-adress is a 32-bit number divided into 4 "blocks", each 8 bits.<br>
`192.168.100.1` turns into `11000000.10101000.01100100.00000001`.<br>
The min value of each "block" is `0` and the max value is `255`.<br>
- The first address in a subnet is used to identify the subnet itself. In this address all host bits are 0. To avoid ambiguity in representation, this address is reserved.
- The last address has all host bits set to 1. It is used as a local broadcast address for sending messages to all devices on the subnet simultaneously.
NOTE: However, this does not mean that every address ending in `0` or `255` cannot be used as a host address. For example, in the/16 subnet `192.168.0.0/255.255.0.0`, which is equivalent to the address range `192.168.0.0 – 192.168.255.255`, the broadcast address is `192.168.255.255`. One can use the following addresses for hosts, even though they end with 255: `192.168.1.255`, `192.168.2.255`, etc. Also, `192.168.0.0` is the network identifier and must not be assigned to an interface, but the addresses `192.168.1.0`, `192.168.2.0`, etc., may be assigned, despite ending with `0`.

### Private networks
Of the approximately four billion addresses defined in IPv4, about 18 million addresses in three ranges are reserved for use in private networks. Packets addresses in these ranges are not routable in the public Internet; they are ignored by all public routers. Therefore, private hosts cannot directly communicate with public networks, but require network address translation at a routing gateway for this purpose.

| Name | CIDR block | Adress range |
| :--: | :--------: | :----------: |
| 24-bit block | `10.0.0.0/8` | `10.0.0.0 – 10.255.255.255` |
| 20-bit block | `172.16.0.0/12` | `172.16.0.0 – 172.31.255.255` |
| 16-bit block | `192.168.0.0/16` | `192.168.0.0 – 192.168.255.255` |

Loopback (also written loop-back) is the routing of electronic signals or digital data streams back to their source without intentional processing or modification. It is primarily a means of testing the communications infrastructure. For this purpose, the following IP adresses are reserved:

| Name | CIDR block | Adress range |
| :--: | :--------: | :----------: |
| localhost | `127.0.0.0/8` | `127.0.0.0 – 127.255.255.255` |


## Network Mask
The mask is used to define which range of ip-adresses are part of the same subnet.

### Mask Structure
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

### CIDR notation
CIDR notation is a compact representation of an IP address and its associated network mask.
CIDR notation specifies an IP address, a slash ('/') character, and a decimal number.
The decimal number is the count of consecutive leading 1-bits (from left to right) in the network mask. The number can also be thought of as the width (in bits) of the network prefix. 

## IP vs Mask

The more usable ip-addresses you need in one subnet, the less subnets you will be able to create.<br>

| CIDR | Dot-decimal | Number of IP-addresses<br /> per subnet | Usable IP-addresses <br /> per subnet | Number of subnets |
| :---: | :-----------: | :---: | :---: | :---: |
| /32 | `255.255.255.255` | 1 | 0 | 256 |
| /31 | `255.255.255.254` | 2 | 0 | 128 |
| /30 | `255.255.255.252`| 4 | 2 | 64 |
| /29 | `255.255.255.248` | 8 | 6 | 32 |
| /28 | `255.255.255.240` | 16 | 14 | 16 |
| /27 | `255.255.255.224` | 32 | 30 | 8 |
| /26 | `255.255.255.192` | 64 | 62 | 4 |
| /25 | `255.255.255.128` | 128 | 126 | 2 |
| /24 | `255.255.255.0` | 256 | 254 | 1 |

### Subnet Mask Chart
Here is a quick reference table for help when subnetting.
|Subnet Mask 	|CIDR |	Binary Notation| 	Network Bits| 	Host Bits| 	Available Addresses|
| -           | -   | -              | -            | -          | -                   | 
|255.255.255.255| 	/32| 	11111111.11111111.11111111.11111111| 	32| 	0| 	1|
|255.255.255.254| 	/31| 	11111111.11111111.11111111.11111110| 	31| 	1| 	2|
|255.255.255.252| 	/30| 	11111111.11111111.11111111.11111100| 	30| 	2| 	4|
|255.255.255.248| 	/29| 	11111111.11111111.11111111.11111000| 	29| 	3| 	8|
|255.255.255.240| 	/28| 	11111111.11111111.11111111.11110000| 	28| 	4| 	16|
|255.255.255.224| 	/27| 	11111111.11111111.11111111.11100000| 	27| 	5| 	32|
|255.255.255.192| 	/26| 	11111111.11111111.11111111.11000000| 	26| 	6| 	64|
|255.255.255.128| 	/25|     11111111.11111111.11111111.10000000| 	25| 	7| 	128|
|255.255.255.0| 	/24| 	11111111.11111111.11111111.00000000| 	24| 	8| 	256|		
|255.255.254.0| 	/23| 	11111111.11111111.11111110.00000000| 	23| 	9| 	512|
|255.255.252.0| 	/22| 	11111111.11111111.11111100.00000000| 	22| 	10| 	1024|
|255.255.248.0| 	/21| 	11111111.11111111.11111000.00000000| 	21| 	11| 	2048|
|255.255.240.0| 	/20| 	11111111.11111111.11110000.00000000| 	20| 	12| 	4096|
|255.255.224.0| 	/19| 	11111111.11111111.11100000.00000000| 	19| 	13| 	8192|
|255.255.192.0| 	/18| 	11111111.11111111.11000000.00000000| 	18| 	14| 	16384|
|255.255.128.0| 	/17| 	11111111.11111111.10000000.00000000| 	17| 	15| 	32768|
|255.255.0.0| 	/16| 	11111111.11111111.00000000.00000000| 	16| 	16| 	65536|	
|255.254.0.0| 	/15| 	11111111.11111110.00000000.00000000| 	15| 	17| 	131072|
|255.252.0.0| 	/14| 	11111111.11111100.00000000.00000000| 	14| 	18| 	262144|
|255.248.0.0| 	/13| 	11111111.11111000.00000000.00000000| 	13| 	19| 	524288|
|255.240.0.0| 	/12| 	11111111.11110000.00000000.00000000| 	12| 	20| 	1048576|
|255.224.0.0| 	/11| 	11111111.11100000.00000000.00000000| 	11| 	21| 	2097152|
|255.192.0.0| 	/10| 	11111111.11000000.00000000.00000000| 	10| 	22| 	4194304|
|255.128.0.0| 	/9| 	11111111.10000000.00000000.00000000| 	9| 	23| 	8388608|
|255.0.0.0| 	    /8| 	11111111.00000000.00000000.00000000| 	8| 	24| 	16777216| 

## Switches
A switch will enable you to connect more than two devices to the same network.<br>
Its only purpose is to distribute packages to its network.<br>


## Routers
As previously mentioned a router is an interface which enables communication between different networks.<br>
A router has the ability to be part of multiple networks, in Netpractice this is visualized by the so called `Interface`.<br>
If routers and switches are still magic to you, I suggest looking deeper [into it](https://www.youtube.com/watch?v=Vc16CCAAz7Q) yourself, as their basic understanding is crucial to succeed in this project.


[back to contents](https://github.com/tblaase/Net_Practice#contents)

## Routing Table


![example_router](https://github.com/tblaase/Net_Practice/blob/main/readme_additions/router_example.png)


The routing table is there to store all the different paths to all the networks, the device is part of.<br>
In Net_Practice the routing table consists of two elements, the **destination** and the **next hop**<br>
The **destination** consists of the network-address that you want to send a package to, combined with the CIDR of that network: `190.3.2.252/30`. If you don't want to specify a destination, you can just set it to `default` or `0.0.0.0/0`.<br>
The **next hop** is the address of the next router that you need to send the packages to in order to reach the destination-network.<br>


[back to contents](https://github.com/tblaase/Net_Practice#contents)

## Network

And now to connect all of the above mentioned topics.<br>
In order to have a functioning network, you now need to apply all of the parts talked about earlier.<br>
If there should be a working connection in a network, the devices somehow need to be connected, either directly or with the help of routers which are part of both networks.


Now you may ask, how do I know if two devices are part of the same network?<br>
For this you need to combine the IP-address and the mask of the devices in order to get the network-adress, that device is part of.<br>
By combining I mean, doing a bit-by-bit-AND-opperation.<br>
For that we first need to translate the IP and the mask to binary.<br>
i.e.:<br>
IP: `192.168.100.1` in binary: `11000000.10101000.1100100.00000001`<br>
MASK: `255.255.255.0` in binary: `11111111.11111111.11111111.00000000`<br>
Now you just combine the two bit by bit, if both bits are a `1` the corresponding bit of the network-address is `1`, in any other case the corresponding bit is `0`.


By doing that to the mentioned example, you should get the network-address of<br>`11000000.10101000.1100100.00000000` in binary or `192.168.100.0` in dot-decimal.<br>
If two devices share the same network-address, they are part of the same network and communication is ensured.