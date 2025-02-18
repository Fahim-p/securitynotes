---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/secure-network-architecture/","created":"2025-02-16T16:21:50.446-05:00","updated":"2025-02-16T19:50:45.318-05:00"}
---

# Task 2 - Network Segmentation

- VLANS are used to segment portions of a network and split devices
	- Adds tags to a frame, designates where traffic originated from
- Native VLAN
	- Used for any untagged traffic that goes through a switch
- Tagged frames can only communicate with the same tagged devices
- Switch port
	- Designated interface for VLANs to traverse through on a switch
- Trunk
	- Connection between switch and router
- ROAS
	- Router on a stick design
	- Way for VLANs to be routed through one router and multiple switches
- Virtual Sub-interfaces
	- Done since all tagged traffic comes from a single connection
	- Allows for routers to keep each tagged frame separate
	- Acts like physical interfaces, defined by VLAN ID

> [!VLAN Configuration]
> 
> ```bash
> / # ovs-vsctl show
> 87c2a3ee-5374-435a-81c2-e8aafa96e3b9
>     Bridge br2
>         datapath_type: netdev
>         Port br2
>             Interface br2
>                 type: internal
>     Bridge br1
>         datapath_type: netdev
>         Port br1
>             Interface br1
>                 type: internal
>     Bridge br0
>         datapath_type: netdev
>         Port eth9
>             tag: 30
>             Interface eth9
>         Port br0
>             Interface br0
>                 type: internal
>         Port eth13
>             tag: 30
>             Interface eth13
>         Port eth14
>             tag: 30
>             Interface eth14
>         Port eth15
>             tag: 30
>             Interface eth15
>         Port eth2
>             tag: 10
>             Interface eth2
>         Port eth8
>             tag: 30
>             Interface eth8
>         Port eth3
>             tag: 20
>             Interface eth3
>         Port eth7
>             tag: 30
>             Interface eth7
>         Port eth4
>             tag: 20
>             Interface eth4
>         Port eth10
>             tag: 30
>             Interface eth10
>         Port eth5
>             tag: 20
>             Interface eth5
>         Port eth6
>             tag: 30
>             Interface eth6
>         Port eth12
>             tag: 30
>             Interface eth12
>         Port eth0
>             Interface eth0
>         Port eth11
>             tag: 30
>             Interface eth11
>         Port eth1
>             tag: 10
>             Interface eth1
>     Bridge br3
>         datapath_type: netdev
>         Port br3
>             Interface br3
>                 type: internal
> ```
> 

> [!Question]
> **How many trunks are present in this configuration?**

Count all "Bridge" interfaces
 
> [!done] Answer
> 4

> [!Question]
> **What is the VLAN tag ID for interface eth12?**

> [!done] Answer
> 30

# Task 3 - Common Secure Network Architecture

- Focus on security, optimization, and redundancy when designing a network
- Security zones
	- Defines what/who is in a VLAN and how traffics goes in/out

| **Zone**           | **Explanation**                                                                                                                            | **Examples**                              |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------- |
| External                 | All devices and entities outside of our network or asset control.                                                                                | Devices connecting to a web server        |
| DMZ (demilitarized zone) | Separates untrusted networks or devices from internal resources.                                                                                 | BYOD, remote users/guests, public servers |
| Trusted                  | Internal networks or devices. A device may be placed in the trusted zone if there is no confidential or sensitive information.                   | Workstations, B2B                         |
| Restricted               | Any high-risk servers or databases.                                                                                                              | Domain controllers, client information    |
| Management               | Any devices or services dedicated to network or other device management. This zone is less commonly seen and can be grouped with the audit zone. | Virtualization management, backup servers |
| Audit                    | Any devices or services dedicated to security or monitoring. This zone is less commonly seen and can be grouped with management.                 | SIEM, telemetry                           |

- Need to factors rules when seeing how new traffic enters network, be assigned, and interact with other/internal systems
	- Can create access control rules based on traffic specifics (MAC, IP address, etc)

> [!Question]
> **From the above table, what zone would a user connecting to a public web server be in?**

> [!done] Answer
> External

> [!Question]
> **From the above table, what zone would a public web server be in?**

> [!done] Answer
> DMZ

> [!Question]
> **From the above table, what zone would a core domain controller be placed in?**

> [!done] Answer
> Restricted
# Task 4 - Network Security Policies and Controls

- Policies aid in showing how network traffic is controlled
- Traffic filtering
	- ACL (Access Control List)
		- Contains ACE (Access Control entry)/rules that defines a list based on pre-defined criteria
			- Determines action, destination/source, and address/range to trigger ACE
		- Used for traffic filtering, priority, customer queuing, or dynamic access control
	- Provides network security, validation, and segmentation through filtering network traffic based on pre-defined criteria

> [!Task] Analyzing Packets and ACLS
> Look at the following 2 packets to answer the questions

> [!Packet 1 with ACL policy] Packet 1 with ACL policy
> 
> ```bash
> Internet Protocol Version 4, Src: 10.10.212.209, Dst: 10.10.212.209
>     Protocol:TCP (6)
>     Header checksum: 0xbfdd [validation disabled]
>     [Header checksum status: Unverified]
>     Source: 10.10.212.209
>     Destination: 10.10.212.209
> Transmission Control Protocol, Src Port: 35560, Dst Port: 22, Seq: 1578, Ack: 1670, Len: 148
>     Source Port: 35560
>     Destination Port: 22
> ```
> 
> `set policy access-list 1 rule 1 action permit`
> 
> `set policy access-list 1 rule 1 source 255.255.255.0`
> 
> `set policy access-list 1 rule 1 source 10.10.212.0/24`
> 

> [!Packet 2 with ACL Policy] Packet 2 with ACL policy
> 
> ```bash
> Internet Protocol Version 4, Src: 10.10.212.200, Dst: 10.10.212.209
>     Protocol:TCP (6)
>     Header checksum: 0xbfdd [validation disabled]
>     [Header checksum status: Unverified]
>     Source: 10.10.212.209
>     Destination: 10.10.212.209
> Transmission Control Protocol, Src Port: 35560, Dst Port: 22, Seq: 1578, Ack: 1670, Len: 148
>     Source Port: 35560
>     Destination Port: 2
> ```
> 
> `set policy access-list 1 rule 1 action deny`
> 
> `set policy access-list 1 rule 1 destination 10.10.212.209`
> 


> [!Question]
> **According to the corresponding ACL policy, will the first packet result in a drop or accept?**

Source of packet matches last rule, resulting in accept

> [!done] Answer
> Accept

> [!Question]
> **According to the corresponding ACL policy, will the second packet result in a drop or accept?**

Destination address matches last rule, resulting in drop

> [!done] Answer
> Drop

# Task 5 - Zone-Pair Policies and Filtering

- Network considerations
	- Size, traffic, data correlation
- Traffic correlation
	- Standardizing state of a packet (port, process, direction)
- Firewall
	- Stateful
		- Better correlate information in network connection
		- Can filter based of protocols, ports, process, or other info from device
	- Stateless
- Zone-pair
	- Direction-based stateful policy that enforces traffic in single directions per VLAN
		- DMZ -> LAN or LAN -> DMZ
	- Each zone should have a different zone-pair for each other in all possible directions
	- Gives most visibility for a firewall and improves filtering capabilities

| **Zone A** | **Zone B** | **Protocol** | **Action** |
| ---------- | ---------- | ------------ | ---------- |
| LAN        | WAN        | ICMP         | Drop       |
| LAN        | LOCAL      | -            | -          |
| LAN        | DMZ        | -            | -          |
| WAN        | LAN        | ICMP         | Accept     |
| WAN        | LOCAL      | -            | -          |
| WAN        | DMZ        | -            | -          |
| LOCAL      | LAN        | -            | -          |
| LOCAL      | WAN        | -            | -          |
| LOCAL      | DMZ        | -            | -          |
| DMZ        | LAN        | HTTP         | Accept     |
| DMZ        | WAN        | -            | -          |
| DMZ        | LOCAL      | -            | -          |


> [!Task] Creating Zone-Pair from Scratch
> Look at the tables below to fill out the table shown on the website to get the flag

| Source | Destination | Protocol | Action | Default Action |
| ------ | ----------- | -------- | ------ | -------------- |
| DMZ    | LAN         | HTTP     | Accept | Drop           |
| DMZ    | WAN         | -        | -      | Drop           |
| LAN    | DMZ         | ICMP     | Accept | Drop           |
| WAN    | DMZ         | -        | -      | Drop           |

| Common Name | Interface | Default Action |
| ----------- | --------- | -------------- |
| DMZ         | eth0.10   | Drop           |
| LAN         | eth0.20   | Drop           |
| WAN         | eth0.30   | Drop           |

![](/img/user/TryHackMe/THM_Images/Pasted image 20250216193304.png)

> [!Question]
> **What is the flag found after filling in all blanks on the static site?**

Fill out the blanks

![](/img/user/TryHackMe/THM_Images/Pasted image 20250216193633.png)

> [!done] Answer
> THM{M05tly_53cure}

# Task 6 - Validating Network Traffic

- SSL/TLS Inspection
	- Uses an SSL proxy to intercept protocols, any encrypted traffic
	- Decrypts intercepted traffic and sent to UTM (Unified Threat Management) platform
		- Performs deep SSL inspection and other services to process info
	- Requires a SSL proxy or Man-in-the-Middle
	- Not 100% solution if vendor implemented
		- Could retrieve plaintext passwords

> [!Question]
> **Does SSL inspection require a man-in-the-middle proxy? (Y/N)**

> [!done] Answer
> Y

> [!Question]
> **What platform processes data sent from an SSL proxy?**

> [!done] Answer
> Unified Threat Management
# Task 7 - Addressing Common Attacks

- DHCP Snooping
	- Security feature that's like a firewall between untrusted hosts and trusted DHCP servers
	- Validates and rate-limits DHCP traffic if necessary
		- If host is untrusted, then it filters the traffic/rate-limits it
	- Operates at the switch layer
	- DHCP Binding Database
		- Stores untrusted hosts with leased IP addresses
		- Used to validate traffic, can be used by other protocols
	- List of conditions to dropping a packet
		- Is received from outside of the network.
		- Source MAC address and DHCP client hardware address don't match.
		- A DHCPRELEASE or DHCPDECLINE packet is received on an untrusted interface that does not match an interface that the source address already has registered.
		- A DHCP packet that includes a relay agent address that is not 0.0.0.0
- Dynamic ARP Inspection
	- Security feature that validates Address Resolution Protocol (ARP) packets in a network
	- Validates and rate-limits ARP packets if needed
	- If ARP packets MAC and IP don't match, then it'll intercept, log, and discard packet
	- Uses DHCP binding database as its list of binding IP addresses

> [!Question]
> **Where does DHCP snooping store leased IP addresses from untrusted hosts?**

> [!done] Answer
> DHCP Binding Database

> [!Question]
> **Will a switch drop or accept a DHCPRELEASE packet?**

> [!done] Answer
> Drop

> [!Question]
> **Does dynamic ARP inspection use the DHCP binding database? (Y/N)**

> [!done] Answer
> Y

> [!Question]
> **Dynamic ARP inspection will match an IP address and what other packet detail?**

> [!done] Answer
> MAC Address
