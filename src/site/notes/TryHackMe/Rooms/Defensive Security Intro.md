---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/defensive-security-intro/","created":"2024-12-03T17:43:00.000-05:00","updated":"2025-03-09T16:38:29.627-04:00"}
---

# Task 1 - Introduction to Defensive Security

> [!Question]
>  **Which team focuses on defensive security?**

> [!Success] Answer
> Blue Team


# Task 2 - Areas of Defensive Security

- **SOC Areas of Interest**
	- Vulnerabilities
	- Policy violations
	- Unauthorized security
	- Network Intrusions
- **Threat Intelligence**
	- Collecting information to better prepare against potential adversaries
		- Achieve threat-informed defense
	- Data collected from local sources
		- Network logs and forums
- **Digital Forensics and Incident Response (DFIR)**
	- **Digital forensics**
		- Analyzing evidence of attack and it's perpetrators
		- Checks for areas like file systems, system memory, and system/network logs
	- **Incident response**
		- Methodologies employed by the blue team on how they would respond to a cyber attack/ data breach
		- Reduce damage and recover ASAP
		- **4 major hases**
			- Preparation
			- Detection and Analysis
			- Containment, Eradication, and Recovery
			- Post-Incident Activity
		- **Malware analysis**
			- Malicious software such as viruses, trojan horse, and ransomware
			- Aims to learn through
		- **Static analysis**
			- Inspecting malicious program without running it
			- Dynamic analysis
			- Running malware in controlled environment and monitoring its activities

> [!Question] 
**What would you call a team of cyber security professionals that monitors a network and its systems for malicious events?**

> [!Success] Answer 
Security Operations Center

> [!Question] 
**What does DFIR stand for?**

> [!Success] Answer
Digital Forensics and Incident Response

> [!Question] 
**Which kind of malware requires the user to pay money to regain access to their files?**

> [!Success] Answer
Ransomware
# Task 3 - Practical Example of Defensive Security

- Clicked on the website to get to this static page

![1000](/img/user/TryHackMe/THM_Images/d148c76efc582365c1e5ea18e4189acd.png)

Noticed the second message looked off, with a unauthorized connection attempt from the IP address 143.110.250.149 to port 22

![1000](/img/user/TryHackMe/THM_Images/66ab668ad4d9ebc6a6c9cad9c9b902e3.png)

Clicking on it brings us to the next part, asking us to scan for any Ips through a IP scanner website.

![1000](/img/user/TryHackMe/THM_Images/ad592be8767bb909b90455a35c4e1a14.png)

Putting in the IP address noted earlier (143.110.250.149) gives us the message that it's actually a known malicious address

![1000](/img/user/TryHackMe/THM_Images/7990bcecb9729bd38bcbeb12039e418c.png)

![1000](/img/user/TryHackMe/THM_Images/3190399fa6a415867844f3957748ad2f.png)

Now that we have the known malicious IP address, we can escalate the issue to a staff member.

![1000](/img/user/TryHackMe/THM_Images/25c1f906ff75387dbb53647619970887.png)

Decided to go for Will, since he's the SOC Team Lead which would be the logical next step up from our position as a SOC analyst. Doing so brings us to the firewall block list page, where we're able to block any IP addresses that we put into the text bar.

![1000](/img/user/TryHackMe/THM_Images/f9eca388bd9ba2e4c2ce7191e459b320.png)

We can put in the malicious IP address noted earlier (143.110.250.149) and click the button.

![1000](/img/user/TryHackMe/THM_Images/9347ec009b8c4ae89c5cb4071761d459.png)

Doing so gives us the flag.

![1000](/img/user/TryHackMe/THM_Images/e86cbc40aad4ac73aa545ae302286f5f.png)

> [!Question] 
**1. What is the flag that you obtained by following along?**

> [!Success] Answer
THM{THREAT-BLOCKED}