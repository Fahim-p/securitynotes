---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/network-security-protocols/","created":"2025-02-19T18:08:51.497-05:00","updated":"2025-03-11T00:32:59.316-04:00"}
---

# Task 2 - Network Security Protocols

- **HTTPS Protocol**
	- Client-server protocol; responsible for securely sending data between a web server (website) and a web browser (client side). 
	- Developed to securely share sensitive information, including passwords, contact information and financial information, between web browsers and websites. 
	- **Workflow - HTTPS**
		- HTTPS adds a layer of encryption to HTTP through SSL/TLS (Secure Sockets Layer/Transport Layer Security). 
		- Still works the same as HTTP
	- **Request and Response - HTTP**
		- An HTTP request is made by a user agent through a web API 
			- Calls like `GET`, `PUT`, or `POST`
			- It is vice versa in the case of response. 
		- Aims to access some resources on the remote web server, which is then responded to by the web server.
		- If an attacker can capture the network packets between the client and the server, they will be able to read their content as it is sent in cleartext.
	- **Request and Response - HTTPS**
		- Attackers will fail to read the contents of the TCP data due to encryption if they capture the packets during transmission.
	- **Encryption Mechanism of HTTPS**
		- As already mentioned, SSL/TLS provides the encryption layer of HTTPS. 
		- It relies on asymmetric encryption (public key cryptography) and symmetric encryption.
		- The default port of HTTPS is 443.
- **FTPS Protocol**
	- **Technical Overview - FTPS**
		- Communication protocol which is a refined and secure version of File Transfer Protocol (FTP).
		- Client-server model; separate control/command and data connections between a client and a server are used, along with a username and password. 
	- **Workflow**
		- FTPS is an extension of FTP, which adds TLS security to commands and data connections.
	- **Request and Response - FTP**
		- Utilizes the following two communication channels between the client and the server.
			- **Control Connection** 
				- FTP client sends a connection request (authentication) to the remote FTP server at the default FTP port, TCP port 21. 
				- Used for sending and receiving commands and responses.
			- **Data Connection:** 
				- After authentication, this connection is used for transferring data (files and folders).
	- **FTP Connection Types**
		- **Active mode**
			- The FTP client connects to the FTP server at TCP port 21 to establish a command connection.
			- The FTP server connects to the FTP client at TCP port 20 to establish a data connection.
			- Unsuitable if client is behind a firewall, as it will block incoming connections to the client.
		- **Passive mode**
			- Client establishes the control and data connections. 
				- Client sends the `PASV` command to the server over the command channel 
				- Server sends a random port to the client. 
			- As soon as the client receives the port number, the client establishes a connection to the provided port number so that the server can initiate the data transfer.
			- This type of connection works well when the client is behind the firewall.
	- **FTP Data Types**
		- **ASCII/Type A**
			- Default type and is used for text file transfers. 
			- If necessary, data is converted into 8-bit ASCII before transmission and then converted back upon reception.
		- **Image/Type I**
			- Referred as binary mode. 
			- It uses byte-by-byte transmission. The recipient stores the received bytes upon reception.
		- **EBCDIC/Type E**
			- Made for text communication using the EBCDIC character set.
		- **Local Type L n**
			- Used for file transfer among machines that do not support 8-bit bytes transfer. 
			- Here `n` is a second parameter that represents byte size. 
	- **Request and Response - FTPS**
		- **Implicit Connection**
			- FTPS client and server establish a link in which both command and data channels are secured automatically with SSL encryption.
		- **Explicit Connection**
			- The FTP client explicitly requests the server to invoke an SSL/TLS secured session on port 21 and then continue data transfer based on a mutually agreed authentication mechanism. 
			- Can choose which channel to encrypt by choosing among three modes of communication for control and data channel, 
				- Control only encrypted, data only encrypted and both control and data encrypted.
		- The standard port for FTP and Explicit FTPS is 21, whereas it is 990 in the case of Implicit FTPS. 
- **SMTPS Protocol**
	- **Technical Overview**
		- Used for email communication.
		- Not the same as POP3. 
			- SMTP is an “Email Push Protocol” used to transfer email messages from the client to the server. 
			- POP3 is used to download email messages from the server to the client. 
	- **SMTP Protocol**
		- **SMTP End-to-End** 
			- Used between organizations
			- Sender-side SMTP client initiates an SMTP connection to the recipient’s SMTP server.
		- **SMTP Store-and-Forward** 
			- Used within an organization
			- SMTP server will maintains a copy of the mail within itself until the copy is forwarded to the receiver.
	- **SMTP Components**
		- **User Agent (UA)** 
			- Creates the email message and sending it to the Mail Transfer Agent (MTA).
		- **Mail Transfer Agent (MTA)** 
			- Transfers the email from the UA to the recipient MTA across the Internet
	- **TLS Process in SMTPS**
		- SMTPS is not a proprietary protocol; instead, it wraps SMTP inside TLS.
			- Similar to SMTP on the application layer
		- Port 587 and 465 are both frequently used for SMTPS traffic. 
		- Forbids attackers from sending spam messages from compromised/vulnerable domains, exfiltration sensitive information, and conducting phishing attacks.
- **POP3S Protocol**
	- **Technical Overview - POP3S**
		- Used for the encrypted retrieval of email messages from the email server to the email client. 
	- **POP3 Protocol**
		- Retrieves email messages from a Mail Delivery Agent (MDA) to a Mail User Agent (MUA).
	- **POP3 Components and Workflow**
		- Two components: client (MUA) and server (MDA).
			- The email client establishes a connection to the email server.
			- The email client downloads all the queued emails from the email server.
			- All emails are saved on the device that initiated the connection.
			- The email server deletes the email copy.
	- **Limitations of POP3**
		- **Emails are Processed Locally** 
			- No synchronization of email messages across multiple devices. 
			- Protocol downloads the emails on the currently logged-in device and usually deletes them from the server.
		- **Transmission in clear text** 
	- **POP3S**
		- Wraps the communications related to email messages from POP3 within TLS. 

> [!Question]
>  **What is the default port for HTTPS?**

> [!Success] Answer
> 443

> [!Question]
>  **In a passive FTP connection, what does the client send the first command over the command channel?**

> [!Success] Answer
> PASV

> [!Task]
>  **Use the [SSL Shopper](https://www.sslshopper.com/ssl-checker.html) website to check the SSL certificate of [TryHackMe](https://www.tryhackme.com/).**

![](/img/user/TryHackMe/THM_Images/fec202c274e629cbf538413847013cce.png)

> [!Task]
>  **Open the [SuperTool](https://mxtoolbox.com/SuperTool.aspx) website, select the Test Email Server option, and check the SMTP Security for smtp.gmail.com.**

![](/img/user/TryHackMe/THM_Images/6115bfa3eab2ec5bc8df9a3755a78125.png)

# Task 3 - Application Layer - More Secure Protocols

- **DNSSEC**
	- DNS protocol is responsible mainly for resolving domain names from IP addresses.
	- DNS works by a client sending a DNS query. 
		- For instance, when browsing the web, your web browser might send a query for DNS record type `A` or `AAAA`,
		- The DNS server responds with the following DNS record type.
	- This name-to-IP address resolution is very convenient
		- However, can easily be spoofed, client would've accepted any response 
	- DNSSEC makes it possible to ensure that the DNS response we receive is from the domain owner.
		- The DNS zone owner should sign all DNS records using their private key.
		- The DNS zone publishes its public key so users can check the validity of the DNS records signatures.
	- With signed records, DNSSEC provides the following
		- **Authenticity** 
			- You can confirm that a certain DNS owner has authored and sent the record. 
			- Possible because the received record is signed by the DNS owner’s private key.
		- **Integrity** 
			- You can ensure that no changes have been made to the record on its way. 
			- Any changes to the record will render its signature invalid.
- **OpenPGP**
	- Protocols like SMTP, POP3, and IMAP are all sent in cleartext, easy for others to see
		- IMAP, allows for synchronization of your mailbox to a server
	- Users started to connect to a web server to read and compose their email messages.
		- The web server uses a mail server to send composed email messages and receive incoming ones.
		- Done over HTTP
	- HTTPS became the new standard. 
		- Traffic between the web browser and the web server to be encrypted. 
		- However, the email traffic is not necessarily encrypted between the web server and the mail server(s). 
			- The web server and mail servers can read the contents of the messages;
	- Eventually, SSL/TLS started to find their way into all email protocols. 
		- However, the mail server can read the email message contents.
		- Need to find a way to trust mail servers along the way
	- PGP (Pretty Good Privacy) is an encryption program used to solve this problem. 
		- OpenPGP is an **open standard** for signing and encrypting files and email messages
		- GnuPG (Gnu Privacy Guard), or simply GPG, is a free and open-source implementation of the OpenPGP standard. 
			- Allows you to sign and encrypt your data and communications.
	- Integrates with your mail client to seamlessly sign, encrypt and decrypt email messages. 
	- Email messages encrypted using OpenPGP is only readable by the intended recipient. 
		- No one, including the mail servers, can read the contents of the messages except the intended recipient.
	- When used with email, GnuPG requires each user to generate a key pair: a private key and a public key. 
		- Sender’s private key is used for signing, 
		- Recipient’s public key is used for encryption. 
		- Sender’s public key is used to check the signature
		- Recipient’s private key is used for decryption. 
	- Protects the confidentiality and integrity of email message contents. 
		- However, this does not include email message headers.
	- To use OpenPGP, both parties need to generate a key pair using the command `gpg --gen-key`. 
		- Asks the user to provide their name and email address and create a private and public key. 
			- Private key should be stored securely 
			- Public key should be shared with the other parties
	- `gpg --encrypt --sign --armor -r strategos@tryhackme.thm message.txt`
		- `--encrypt -r recipient@tryhackme.thm` will encrypt `message.txt` using the public key associated with the recipient’s email. This will provide confidentiality.
		- `--sign` will sign our message (using our private key). This will prove authenticity.
		- `--armor` is to produce the output using ASCII instead of binary.

> [!Question]
>  **What does PGP stand for?**

> [!Success] Answer
> Pretty Good Privacy

> [!Question]
>  **What does GPG stand for?**

> [!Success] Answer
> Gnu Privacy Guard

> [!Question]
>  **What command would you use to generate a key pair using `gpg`?**

> [!Success] Answer
> `gpg --gen-key`

> [!Question]
>  **Consider the following three clients:
1.`rlogin`
2.`telnet`
3.`ssh`
Provide the number of the client that encrypts the traffic**

> [!Success] Answer
> 3

# Task 4 - Presentation and Session Layers

- **SSL/TLS Protocol**
	- **Technical Overview - SSL/TLS**
		- Protocols used to encrypt data exchanged between a client, such as a web browser, and a server. 
		- Acts like wrapper that encrypts various communication protocols, such as HTTP and FTP, to create HTTPS and FTPS.
	- **SSL/TLS Workflow**
		- **Client Hello Message**
			- The client sends a hello message to the server
			- Has client TLS version and the cypher suite that the client supports, in addition to random bytes.
		- **Server Hello Message**
			- The server responds with a hello message, highlighting its certificate, chosen cypher suite and random bytes.
		- **Authentication**
			- The client authenticates the server’s certificate through the certificate authority that issued it.
			- Received certificate is verified by our browser, which is pre-installed with the certificates of various certificate authorities.
		- **Premaster Secret**
			- The client encrypts random bytes with the server’s public key.
		- **Decryption of Premaster**
			- The server decrypts the premaster with its private key.
		- **Session Keys Generated**
			- The client and the server generate session keys based on client random bytes, random server bytes and premaster secret. 
		- **Ready Messages**
			- Both send a “finished” message using the session key to indicate that the session is ready for transmission
- **SOCKS5 Protocol**
	- **Technical Overview - SOCKS5**
		- Proxy protocol for data exchange through a delegate server (SOCKS5 proxy). 
		- Secures application layer protocols.
	- **SOCKS5 Workflow**
		- Consider a scenario when user A wants to connect with client B over the Internet, but a firewall is between them. 
		- The following handshake steps are involved
			- **Client Initiation**
				- Client A connects with the SOCKS5 proxy and sends the first byte (0x05) to the proxy where “5” is the SOCKS version.
				- Client A sends a second byte (0x01). 
					- One means authentication is supported.
				- Client A sends the third byte (0x00, 0x01, 0x02, or 0x03);
					- Denote the supported authentication methods and can be of variable length.
			- **SOCKS5 Proxy Reply**
				- The proxy sends back a second byte, which is the chosen authentication method by the proxy server.
				- After the initiation packet, client A sends the request packet, 
					- Includes BHOST & BPORT numbers.
				- The successful session is established between client A and the proxy. 
				- The same steps are involved in the association of client B with the proxy.
			- **Data Transfer**
				- After successfully associating both clients with a proxy server, both clients can exchange data and share information that will be routed through the proxy server.
	- **Benefits of SOCKS5**
		- In direct communication via the proxy server, hide the internal details from routing over the Internet.
		- A proxy acts as a relay server, bypassing Internet censorship based on the client’s IP address.


> [!Question]
>  **Does the hello message during the SSL handshake include the TLS version (yea/nay)?**

> [!Success] Answer
> Yea

> [!Question]
>  **During the client initiation process of SOCKS5, what is the SOCKS version if the client sends the first 5 bytes (0x05)?**

> [!Success] Answer
> 5

> [!Question]
>  **Click the View Site button at the top of the task to launch the static site in split view. What is the flag after completing the exercise?**

![](/img/user/TryHackMe/THM_Images/3aaee0128ebb71cba19c699d565c38fb.png)

![](/img/user/TryHackMe/THM_Images/a9bb73e79acfe79ae063cf7771bfc937.png)

![](/img/user/TryHackMe/THM_Images/2a60eea774aa9abb9b357fc8d7ac977b.png)

> [!Success] Answer
> THM{GOT_THE_SSLKEY}

# Task 5 - Network Layer 

- **IPsec (Internet Protocol Security)**
	- Provides security by adding authentication and protecting the integrity and confidentiality of the network traffic
		- **Authentication Header (AH)**
			- Provides authentication and integrity
				- Cannot protect the confidentiality of the data.
			- Transport Mode
				- Provides authentication for the TCP/UDP header and data.
				- Header goes after TCP/UDP header
			- Tunnel Mode
				- Provides authentication for the IP header, TCP/UDP header, and data.
				- Header goes after IP header
		- **Encapsulating Security Payload (ESP)**
			- Provides authentication, integrity, and confidentiality
			- Transport Mode
				- Provides security (confidentiality and integrity) for the TCP/UDP header and data.
				- Header goes before TCP/UDP header, trailer and authentication goes after data
			- Tunnel Mode
				- Provides security (confidentiality and integrity) for the IP header, TCP/UDP header, and data.
				- Header goes before IP header, trailer and authentication goes after data
		- **Security Association (SA):** 
			- Is responsible for negotiating the encryption keys and algorithms
			- One example is Internet Key Exchange (IKE)
- **VPN**
	- Makes it possible to establish a private connection over a public network.
		- Can establish a secure connection over an insecure infrastructure.
	- Requires a VPN client and a VPN server or concentrator. All the traffic between the VPN client and server is encrypted.
	- The two most common protocols used to establish VPN connections are:
		- IPsec
		- SSL/TLS
	- IPsec’s ESP is a perfect protocol for setting up secure tunnels between different networks or a computer and a network. 
		- Can provide security and integrity of all data transmitted between two points
			- Can even hide the IP address in tunnel mode. 
		- Note that the system must be behind a VPN concentrator for the IP address to be hidden.
	- Although SSL was created to secure HTTP traffic, SSL/TLS has found its way to establish secure VPN connections with OpenVPN. 


> [!Question]
>  **What does ESP stand for?**

> [!Success] Answer
> Encapsulating Security Payload

> [!Question]
>  **Which protocol does the Cisco VPN client use to establish a VPN connection?**

> [!Success] Answer
> Ipsec

> [!Question]
>  **Which protocol does the OpenVPN project use for encryption and authentication?**

> [!Success] Answer
> SSL/TLS
