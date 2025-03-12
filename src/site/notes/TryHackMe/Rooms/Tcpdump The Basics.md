---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/tcpdump-the-basics/","created":"2024-10-25T15:46:36.380-04:00","updated":"2025-03-12T00:21:28.666-04:00"}
---

# Task 2 - Basic Packet Capture

| Command              | Explanation                                                                               |
| -------------------- | ----------------------------------------------------------------------------------------- |
| tcpdump -i INTERFACE | Captures packets on a specific network interface,<br><br>-i any listens on all interfaces |
| tcpdump -w FILE      | Writes captured packets to a file                                                         |
| tcpdump -r FILE      | Reads captured packets from a file                                                        |
| tcpdump -c COUNT     | Captures a specific number of packets                                                     |
| tcpdump -n           | Don’t resolve IP addresses                                                                |
| tcpdump -nn          | Don’t resolve IP addresses and don’t resolve protocol numbers                             |
| tcpdump -v           | Verbose display; verbosity can be increased with -vv and -vvv                             |

> [!Question]
> **What option can you add to your command to display addresses only in numeric format?** 

> [!done] Answer
> -n 
# Task 3 - Filtering Expressions

| Command                                  | Explanation                                                     |
| ---------------------------------------- | --------------------------------------------------------------- |
| tcpdump host IP or tcpdump host HOSTNAME | Filters packets by IP address or hostname                       |
| tcpdump src host IP                      | Filters packets by a specific source host                       |
| tcpdump dst host IP                      | Filters packets by a specific destination host                  |
| tcpdump port PORT_NUMBER                 | Filters packets by port number                                  |
| tcpdump src port PORT_NUMBER             | Filters packets by the specified source port number             |
| tcpdump dst port PORT_NUMBER             | Filters packets by the specified destination port number        |
| tcpdump PROTOCOL                         | Filters packets by protocol; examples include ip, ip6, and icmp |

- Can use the three logical operators (and, or, not)
	- Example, tcpdump host 1.1.1.1 and tcp
		- Captures tcp traffic with host 1.1.1.1

> [!Question]
> **How many packets in traffic.pcap use the ICMP protocol?** 

![Pasted image 20250204163812.png](/img/user/TryHackMe/THM_Images/31650cf2c5554fd45996259c5f3b8790.png)

> [!done] Answer
> 26

> [!Question]
> **What is the IP address of the host that asked for the MAC address of 192.168.124.137?** 

![Pasted image 20250204163902.png](/img/user/TryHackMe/THM_Images/c1f98f87f7f75acea6040dd87fbe87a1.png)

> [!Success] Answer
> 192.168.124.148

> [!Question]
> **What hostname (subdomain) appears in the first DNS query?** 

![](/img/user/TryHackMe/THM_Images/2129c11702fa8d5e2b86df6f5c62f287.png)  

> [!Success] Answer
> mirrors.rockylinux.org
# Task 4 - Advanced Filtering

- Can filter on Length (Bytes) with "greater" or "less"
- Also filter based on binary operations
	- & (AND)
	- | (OR)
	- ! (NOT)
- Header bytes
	- Can filter based on TCP flag fields
		- Command, tcp[tcpflags]
		- Tcp-syn,ac,fin,rst,puch -

> [!Question]
> **How many packets have only the TCP Reset (RST) flag set** 

![](/img/user/TryHackMe/THM_Images/351a566a10f8715feb1f511d9497b6dc.png)

> [!Success] Answer
> 57

> [!Question]
> **What is the IP address of the host that sent packets larger than 15000 bytes?** 

![](/img/user/TryHackMe/THM_Images/22ea8b28260f81a2e4413ba7b2a91af8.png)  

> [!Success] Answer
> 185.117.80.53
# Task 5 - Displaying Packets

| Command     | Explanation                                        |
| ----------- | -------------------------------------------------- |
| tcpdump -q  | Quick and quite: brief packet information          |
| tcpdump -e  | Include MAC addresses                              |
| tcpdump -A  | Print packets as ASCII encoding                    |
| tcpdump -xx | Display packets in hexadecimal format              |
| tcpdump -X  | Show packets in both hexadecimal and ASCII formats |

> [!Question] 
> **What is the MAC address of the host that sent an ARP request?**

![](/img/user/TryHackMe/THM_Images/b2fa16a09dcea0b32c4752883f5683dd.png)

> [!Success] Answer
> 52:54:00:7c:d3:5b
