---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/network-device-hardening/","created":"2025-02-19T15:27:46.065-05:00","updated":"2025-02-19T18:05:51.321-05:00"}
---

# Task 2 - Common Threats and Attack Vectors

- **Endpoint devices** 
	- Any device that can generate or consume data on a network, such as Laptops, Desktops, Smartphones, etc.
	- Typically located at the edge of a network and interact directly with users. 
- **Common Threats and Attack Vectors of Network Devices**  
	- Some common goals of hardening include protection from unauthorized access & attacks/exploits, enforcement of access policies, prevention of data theft, and continuous availability of critical systems.

| **Threat**                      | **Description **                                                                                                                                                                        | **Attack Vector**                                                                                                                                                                                                                                           |
| ------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Unauthorised access**         | Gain unauthorised control of a network device, then the network.                                                                                                                        | - Password attacks (brute force, dictionary & hybrid)<br>- Exploit known vulnerabilities, e.g. RCE<br>- Social Engineering/Phishing attack to trick network administrators into disclosing sensitive information such as usernames and passwords of devices |
| **Denial of Service (DoS)**     | Disruption of critical devices and services to make them unavailable to genuine users.                                                                                                  | - Flooding devices with fake requests<br>- Exploiting vulnerabilities in logical or resource handling<br>- Manipulating network packets                                                                                                                     |
| **Man-in-the-Middle Attacks**   | Intercept the network requests between two parties by masquerading as each other to steal sensitive information or alter/manipulate the requests.                                       | - ARP spoofing<br>- DNS spoofing<br>- Rogue access points                                                                                                                                                                                                   |
| **Privilege escalation**        | Gaining higher-level privileges or rights to perform restricted actions, e.g. accessing sensitive information or executing malicious code.                                              | - Weak passwords or use of the same passwords for user and admin accounts<br>- Exploiting vulnerabilities<br>- Misconfigurations                                                                                                                            |
| **Bandwidth theft/ hotlinking** | Linking a bandwidth-intensive resource (image or video) from an external website to its original website, without permission. This can cause increased traffic to the original website. | - Scraping large volumes of data  <br>    <br>- DoS attacks  <br>    <br>- Malware attacks                                                                                                                                                                  |

> [!Question]
> **The device that is used to control and manage network resource is called?** 

> [!Success] Answer
> Network Device

> [!Question]
> **A threat vector that includes disruption of critical devices and services to make them unavailable to genuine users is called?** 

> [!Success] Answer
> Denial of Service

# Task 3 - Common Hardening Techniques

- **General Techniques**
	- Hardening techniques are meant to reduce the attack surface of a system or network
		- **Updating & Patching**
			- Ensuring the latest version of the OS and underlying applications of all devices and systems
			- Install regular security patches
		- **Disabling unnecessary services & ports**
			- Turn off all unnecessary services and block all ports (physical and virtual) that are not needed for system functionality. 
			- Reduces the attack surface by minimizing the number of entry points an attacker can exploit.
		- **Principle of Least Privilege (POLP)**
			- Restrict users and processes to only the minimum necessary permissions required to perform their functions.
		- **Logs Monitoring**
			- Monitor for unusual activity or security events.
		- **Backup regularly**
			- Take routine backups of systems and configurations as they can help recover from a security incident or system failure.
		- **Enforcing Strong Passwords**
			- Change default login passwords and use strong passwords 
			- Protects against dictionary and brute-force attacks.
		- **Multi-Factor Authentication (MFA)** 
			- Additional security layer requiring two or more types of identification before accessing the account or system. 
- **Importance of Secure Protocols**
	- Secure protocols protects against unauthorized access and data breaches. 
		- Ensures data encryption and cannot be intercepted by malicious actors.
		- Prevent MiTM attacks and other network-based exploits. 
	- Ensures that only authorized personnel can access sensitive information and perform system administration tasks.
	- Necessary security protocols include HTTPS, SSH, SSL/TLS, and IPsec. 
- **Implementation of Monitoring and Logging Controls**
	- Essential for detecting and investigating security incidents, identifying performance issues, and complying with regulatory requirements. 
	- It provides a record of events and activities on the device, which can be used for troubleshooting, forensic analysis, and auditing purposes. The following techniques are generally used for logging:
		- **Syslog**
			- Standardize the transfer of log messages, with the purpose of storing and analyzing log messages to a central server.
		- **SNMP**
			- Traps a notification sent by a network device to a management system when a predefined event occurs.
		- **NetFlow**
			- A protocol used to collect and analyze network traffic data for monitoring and security analysis.
		- **Packet Captures**
			- Capturing network traffic and storing it for analysis using a tool like Wireshark.

> [!Question]
> **Suppose you are configuring a router; which of the following could be considered an insecure protocol:  
A: HTTPS  
B: FTP  
C: SSH  
D: IPsec** 

> [!Success] Answer
> FTP

> [!Question]
> **The protocol for sending log messages to a centralized server for storage and analysis is called?** 

> [!Success] Answer
> Syslog
# Task 4 - Hardening Virtual Private Networks

- **Use strong encryption algorithm**
	- Configure the VPN gateway to use strong encryption to protect data in transit. 
	- The **cipher** directive in the config file can be used to select the encryption scheme.  
- **Keep VPN gateway software up-to-date**
	- Ensure that the VPN gateway software is always updated with the latest security patches and updates.
- **Implement strong authentication**
	- Use strong authentication mechanisms such as a combination of Transport Layer Security (TLS) and a secure hashing algorithm.
	- The `auth` directive specifies the exact algorithm in the OpenVPN configuration file 
- **Change default settings**
	- Change the default usernames and passwords to something unique to reduce the risk of unauthorized access
- **Enable Perfect Forward Secrecy (PFS)**
	- Generates unique session keys for each session to strengthen the security of the VPN connection. 
		- If a hacker successfully obtained a session key, they could not use it to decode more sessions. 
	- Can use the `tls-crypt` directive in the OpenVPN configuration file to enable PFS. 
		- Requires a key that can be generated and should be placed in the same directory on the server. 
		- Choosing the appropriate cipher and auth, like **cipher AES-256-CBC** and **auth SHA 256**, supports PFS if combined with tls-crypt.
- **Dedicated Users for VPN Server**
	- Limit user access by creating a dedicated user account and group with restricted permissions specifically for running the OpenVPN server.


> [!Question]
> **Update the config file to use cipher AES-128-CBC. What is the flag value linked with the cipher directive?** 

![](/img/user/TryHackMe/THM_Images/Pasted image 20250219173210.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250219173253.png)

> [!Success] Answer
> THM{CIPHER_UPDATED_1101}

> [!Question]
> **Update the config file to use auth SHA512. What is the flag value linked with the auth directive?**

Refer to previous screenshot

> [!Success] Answer
> THM{AUTH_UPDATED_123}

> [!Question]
> **As per the config file, what is the port number for the OpenVPN server?** 

Refer to previous screenshot

> [!Success] Answer
> 1194

# Task 5 - Hardening Routers, Switches, and Firewalls

- **Setting up the device**
	- Necessary to fill in all relevant details like hostname, timezone, logging, and more. 
		- Assist in conducting incident handling in case of a compromise. 
	- For example, logging must be enabled to log all the events with the default alert level `Debug`. 
		- Similarly, time zone and time synchronization must be set accurately to properly correlate events with their occurrence time.
- **Change default credentials**
	- Usually, the admin web interface is protected through a username and password, and people ignore changing the default. 
		- A threat actor can access the router's admin interface and compromise the whole network using default credentials. 
- **Enable secure network protocols**
	- Maintains the confidentiality, integrity, and availability of network traffic.
		- Secure protocols like HTTPS, SSH, and SSL/TLS offer encrypted authentication mechanisms and communications to stop unauthorized access and eavesdropping. 
	- Reduces the risk of data breaches, man-in-the-middle attacks, and other security threats. 
	- Can add specific public SSH-Keys for passwordless login.
- **Disabling unnecessary scripts**
	- Almost every network device executes some startup scripts to provide a better user experience to a user. 
		- For example, crontab is executed on startup to verify and execute any cron job. 
			- Threat actors try to gain persistent access on a network device by adding their malicious scripts on the startup. 
- **Securing Wi-Fi**
	- If the router has Wi-Fi capabilities, securing the Wi-Fi by enabling strong encryption like WPA2/WPA3, disabling SSID broadcast, changing default passwords, and more.

> [!Question]
> **What is the default SSH port configured for OpenWrt in the attached VM?** 

First logged in with credentials given in the room

![](/img/user/TryHackMe/THM_Images/Pasted image 20250219173901.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250219174141.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250219174222.png)

> [!Success] Answer
> 22


> [!Question]
> **Go through the General Settings option under the System tab in the attached VM. The administrator has left a special message in the Notes section. What is the flag value?** 

![](/img/user/TryHackMe/THM_Images/Pasted image 20250219174249.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250219174344.png)

> [!Success] Answer
> THM{SYSTEM101}

> [!Question]
> **What is the default system log buffer size value for the OpenWrt router in the attached VM?** 

![](/img/user/TryHackMe/THM_Images/Pasted image 20250219174442.png)

> [!Success] Answer
> 64

> [!Question]
> **What is the start priority for the script uhttpd?** 

![](/img/user/TryHackMe/THM_Images/Pasted image 20250219174511.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250219174534.png)

> [!Success] Answer
> 50
# Task 6 - Hardening Routers, Switches, & Firewalls - More Techniques

- **Manage traffic rules**
	- Network devices allow you to create and implement traffic rules that accept/deny network traffic. 
		- For example, we notice that the data of users connected with our network device is being exfiltrated to a command and control server IP address. 
		- Can create a rule to block all traffic where the destination IP matches the attacker's command and control server.
- **Monitor traffic**
	- Keeping track of network traffic, like uploads and downloads of data at different intervals, is essential. 
		- For example, you have excessive data uploaded from one of the email servers to an unknown IP address. 
		- Such alerts enable you to take remedial measures and stop data pilferage timely.
- **Configuring port forwarding**
	- Enables inbound traffic from sources to be routed to a particular device/service on the internal network. 
		- Done through port forwarding rules 
		- Helps host applications that need outside access, granting remote control of internal devices. 
	- Can expose internal devices and services to potential security issues if improperly secured and configured. 
		- Threat actors could add new rules here for creating connections to external command and control servers.
- **Monitoring scheduled tasks**
	- Monitor scheduled tasks to confirm that the original scheduled tasks lists are not modified by a threat actor. 
- **Update firmware**
	- It is essential to update the firmware and installed packages on a regular basis to avoid any know/unknown attacks.
- **Configuring port security**
	- This includes limiting the number of MAC addresses registered on a switch port and taking action against unauthorized access 
	- Tells an administrator that data is coming from a valid source and will be forwarded to a legitimate receiver.
- **Preventing ARP spoofing**
	- Most common vectors for launching man-in-the-middle attacks on the network. 
		- The threat can be mitigated by enabling static ARP tables and implementing MAC address filtering.
- **Preventing rogue DHCP servers**
	- The attacker creates a spoofed DHCP server that can be later on used for assigning IPs to clients and launching MITM attacks. 
	- Mitigation measures to prevent such attacks includes
		- Configuring static DHCP binding
		- Ensuring no unknown devices are added to a network through network mapping tools.
- **Enabling IPv6**
	- Unlike IPv4, IPv6 has built-in support of IPsec that can be used to secure network communication and provide CIA 
		- Protects against MITM, eavesdropping, and tampering of packets in transit.


> [!Question]
> **What is the name of the rule that accepts ICMP traffic from source zone WAN and destination zone as this device?** 

![](/img/user/TryHackMe/THM_Images/Pasted image 20250219175941.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250219180124.png)

> [!Success] Answer
> Host-Centric

> [!Question]
> **What is the name of the rule that forwards data coming from WAN port 9001 to LAN port 9002?** 

![](/img/user/TryHackMe/THM_Images/Pasted image 20250219180220.png)

> [!Success] Answer
> THM_PORT

> [!Question]
> **What is the version number for the available apk package?** 

![](/img/user/TryHackMe/THM_Images/Pasted image 20250219180259.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250219180324.png)

> [!Success] Answer
> 2.12.2-1
