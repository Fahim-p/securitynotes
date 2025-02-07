---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/soc-fundamentals/","created":"2024-11-06T17:24:39.640-05:00","updated":"2025-02-06T21:55:17.910-05:00"}
---

# Task 2 - Purpose and Components

- Main focus is on
	- **Detection**
		- Vulnerabilities
		- Unauthorized activities
		- Policy violations
		- Intrusions
	- **Response**
		- Support incident response team
- Continuous monitoring is required
- 3 Pillars of SOC
	- People
	- Process
	- Technology 

> [!Question]
> **The SOC team discovers an unauthorized user is trying to log in to an account. Which capability of SOC is this?** 

> [!Success] Answer
> Detection
# Task 3 - People

| SOC Level 1        | Anything detected by the security solution would pass through these analysts first. These are the first responders to any detection. Perform basic alert triage to determine if a specific detection is harmful. Also report these detections through proper channels.         |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| SOC Level 2        | Level 2 Analysts help Level 1's dive deeper into the investigations and correlate the data from multiple data sources to perform a proper analysis.                                                                                                                            |
| SOC Level 3        | Proactively look for any threat indicators and support in the incident response activities. Provides detailed responses, including containment, eradication, and recovery from critical severity detections.                                                                   |
| Security Engineer  | Security Engineers deploy and configure these security solutions to ensure their smooth operation.                                                                                                                                                                             |
| Detection Engineer | Security rules are the logic built behind security solutions to detect harmful activities. Level 2 and 3 Analysts often create these rules, while the SOC team can sometimes also utilize the detection engineer role independently for this responsibility.                   |
| SOC Manager        | The SOC Manager manages the processes the SOC team follows and provides support. The SOC Manager also remains in contact with the organization’s CISO (Chief Information Security Officer) to provide him with updates on the SOC team’s current security posture and efforts. |

> [!Question]
> **Alert triage and reporting is the responsibility of?** 

> [!Success] Answer
> SOC Analyst (Level 1)

> [!Question]
> **Which role in the SOC team allows you to work dedicatedly on establishing rules for alerting security solutions?** 

> [!Success] Answer
> Detection Engineer
# Task 4 - Process

- Alert triage
	- Basis of SOC team
	- First response to any alert, analyzing
	- Determines severity and prioritization

Alert: Malware detected on Host: GEORGE PC

| 5 Ws   | Answers                                                                                                                                                                                                                       |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| What?  | A malicious file was detected on one of the hosts inside the organization’s network.                                                                                                                                          |
| When?  | The file was detected at 13:20 on June 5, 2024.                                                                                                                                                                               |
| Where? | The file was detected in the directory of the host: "GEORGE PC".                                                                                                                                                              |
| Who?   | The file was detected for the user George.                                                                                                                                                                                    |
| Why?   | After the investigation, it was found that the file was downloaded from a pirated software-selling website. The investigation with the user revealed that they downloaded the file as they wanted to use a software for free. |

> [!Question]
> **At the end of the investigation, the SOC team found that John had attempted to steal the system's data. Which 'W' from the 5 Ws does this answer?** 

> [!Success] Answer
> Who

> [!Question]
> **The SOC team detected a large amount of data exfiltration. Which 'W' from the 5 Ws does this answer?** 

> [!Success] Answer
> What

# Task 5 - Technology

- **SIEM**
	- Security Information and Event Management
	- Collects logs from devices
	- Set with detection rules to find suspicious activities
	- Gives detections after correlating multiple log sources and alerts
	- Modern implementations give user behaviour analysis and threat intelligence capabilities
- **EDR**
	- Endpoint Detection and Response
	- Real-time and historical visibility of device activities
	- Carries out automated responses
	- Extensive detection capabilities for endpoints
- **Firewall**
	- Barrier between internal and external networks
	- Monitors incoming and outgoing traffic, filters unauthorized traffic
	- Also comes with detection rules

> [!Question]
> **Which security solution monitors the incoming and outgoing traffic of the network?** 

> [!Success] Answer
> Firewall

> [!Question]
> **Do SIEM solutions primarily focus on detecting and alerting about security incidents? (yea/nay)** 

> [!Success] Answer
> Yea

# Task 6 - Practical Exercise of SOC

- Received an alert of port scanning activity for one hosts on the network
- Need to view the logs individually and answer the 5 Ws given below
- Been notified from vulnerability assessment team that they were running a port scan activity inside network from host 10.0.0.8
- Opening up the SIEM gives us to this screen, clicked acknowledge on the alert 167
![Exported image|1000](Exported%20image%2020250204193002-0.png|)

Leads us to this screen to answer the 5Ws 

![Exported image|1000](/img/user/TryHackMe/THM_Images/992dd2b303ad804a05cfd52a5df8c211.png)

> [!Question]
> **What: Activity that triggered the alert?** 

Given the scenario information, we already know that the vulnerability team was running a port scan on this host, which caused the alerts

> [!Success] Answer
> Port Scan

> [!Question]
> **When: Time of the activity?** 

All the alerts were triggered at this time

![Exported image](/img/user/TryHackMe/THM_Images/6d4747f00714ba7d3bcc691791217894.png)  

> [!Success] Answer
> June 12, 2024 17:24

> [!Question]
> **Who: Source host name?** 

We see from the SIEM that the Source Host Name is NESSUS

![Exported image](/img/user/TryHackMe/THM_Images/6066cc15b30e60f0f24f62f56ee1a326.png)  

> [!Success] Answer
> Nessus

> [!Question] 
> **Why: Reason for the activity? Intended/Malicious** 

Once again, we know from the scenario that this was intended as it was from our own vulnerability team, already given notification

> [!Success] Answer
> Intended

> [!Question]
> Additional Investigation Notes: Has any response been sent back to the port scanner IP? (yea/nay) 

We see that at one point, Joe's PC does send back a response to the port scanner IP

![Exported image](/img/user/TryHackMe/THM_Images/b739ad7e4230b1edacdcb5b1a1fe265a.png)  

> [!Success] Answer
> yea

> [!Question]
> **What is the flag found after closing the alert?** 

> [!Success] Answer
> THM{000_INTRO_TO_SOC}      
