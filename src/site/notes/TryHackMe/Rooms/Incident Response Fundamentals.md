---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/incident-response-fundamentals/","created":"2024-11-17T20:53:44.116-05:00","updated":"2025-03-11T00:32:59.192-04:00"}
---

# Task 2 - What are Incidents?

- For anything a process (interactive or not) does, an event is logged
- Many security solutions can handle these events as logs and can find malicious activities in them, triggering alerts
- **False positive**
	- Point to something dangerous but are not harmful
		- Alert on a high amount of data being transferred from one system to an external IP address.
		- Security team found that the subject system was undergoing a backup process to a cloud storage service, which caused this.
- **True positive**
	- Point to something harmful and are actually dangerous
		- Alert on a phishing attempt on one of the organization’s users.
		- Security team found that the email was a phishing email sent to this user to compromise the system
	- Also referred to as incidents
		- Incidents can be categorized as low, medium, high, or critical - 

> [!Question]
> **What is triggered after an event or group of events point at a harmful activity?** 

> [!Success] Answer
> Alert

> [!Question]
> **If a security solution correctly identifies a harmful activity from a set of events, what type of alert is it?** 

> [!Success] Answer
> True positive

> [!Question]
> **If a fire alarm is triggered by smoke after cooking, is it a true positive or a false positive?** 

> [!Success] Answer
> False positive
       
# Task 3 - Types of Incidents

| Malware Infections        | Malicious program that can damage a system, network, or application, majority of incidents.                                                                                                                                                                                   |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Security Breaches         | Happens when an unauthorized person gets access to confidential data.  Utmost importance as many businesses rely on their confidential data                                                                                                                                   |
| Data Leaks                | Incidents in which confidential information of an individual or an organization is exposed to unauthorized entities. reputational damage or threaten their victims and get what they need from them. Can also be unintentionally caused by human errors or misconfigurations. |
| Insider Attacks           | Incidents from within an organization. Can be hazardous, as an insider always has greater access to resources than an outsider.                                                                                                                                               |
| Denial of Service Attacks | Incidents where the attacker floods a system/network/application with false requests, eventually making it unavailable to legitimate users. This happens due to the exhaustion of resources available to entertain the requests.                                              |

> [!Question]
> **A user's system got compromised after downloading a file attachment from an email. What type of incident is this?** 

> [!Success] Answer
> Malware Infection

> [!Question]
> **What type of incident aims to disrupt the availability of an application?** 

> [!Success] Answer
> Denial of Service
     
# Task 4 - Incident Response Process

**SANS Incident Response framework**, PICERL

| Phase           | Explanation                                                                                                                                                                                                             | Example                                                                                                                                                                                                        |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Preparation     | Building the necessary resources to handle an incident.<br><br>Developing incident response teams, having a proper incident response plan in place, and deploying necessary security solutions to combat the incidents. | Conducting awareness training for employees on phishing emails. Phishing emails are fraudulent emails sent by malicious attackers that can trick you into performing actions that can lead you to an incident. |
| Identification  | Looking for any abnormal behavior that may indicate an incident.<br><br>Involves using various security solutions and techniques to monitor abnormal events.                                                            | The security team notices a huge amount of data being sent out from one of the hosts. Upon analysis, it was found to be compromised after a malicious file was downloaded from a phishing email attachment.    |
| Containment     | Minimizing the impact of the attack.<br><br>Usually done by isolating the victim machine, disabling the compromised user accounts, etc.                                                                                 | The Security team isolates the host from the network to minimize the impact and not allow the attacker to jump to other systems, leveraging the compromised host.                                              |
| Eradication     | Removing the threat from the attacked environment.<br><br>Ensures the subject environment is clean                                                                                                                      | A deep malware scan was executed on the system to remove the malicious software from the host.                                                                                                                 |
| Recovery        | Recovering the affected systems from backup or rebuilding them.<br><br>Are then tested and are ready to use.                                                                                                            | The compromised host was re-configured, and the exfiltrated data was restored from the backup.                                                                                                                 |
| Lessons Learned | Gaps in the detection and analysis of the incident are identified and documented, helping to improve the overall process in future incidents.                                                                           | Conducting a post-incident review meeting to analyze the incident's root cause and improve the security to prevent future attacks.                                                                             |

**NIST Framework**, 4 phases        
- Preparation
- Detection and Analysis
- Containment, Eradication, and Recovery
- Post Incident Activity

**Incident Response Plan Components**
- Roles and Responsibilities
- Incident Response methodology
- Communication plan with stakeholders, including law enforcement
- Escalation path to be followed

> [!Question]
> **The Security team disables a machine's internet connection after an incident. Which phase of the SANS IR lifecycle is followed here?** 

> [!Success] Answer
> Containment

> [!Question]
> **Which phase of NIST corresponds with the lessons learned phase of the SANS IR lifecycle?** 

> [!Success] Answer
> Post Incident Activity    

# Task 5 - Incident Response Techniques

Security solutions in detecting incidents

| Security Information and Event Management Solution (SIEM) | Collects all important logs in one centralized location and correlates them to identify incidents.                                   |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Antivirus (AV)                                            | Detects known malicious programs in a system and regularly scans your system for these                                               |
| Endpoint Detection and Response  (EDR)                    | Deployed on every system, protecting it against some advanced-level threats. This solution can also contain and eradicate the threat |

**Playbooks**
- Step-by-step procedure of what to do when dealing with incidents
- Steps may be different per incident type

**Runbooks**
- Detailed, step-by-step execution of specific steps during different incidents.
- These steps may vary depending on the resources available for investigation
    
> [!Question]
> **Step-by-step comprehensive guidelines for incident response are known as?** 

> [!Success] Answer
> Playbooks
  
# Task 6 - Lab Work Incident Response

- Initiate a incident by downloading file from phishing email
- Need to investigate it to answer the following questions

![Exported image](/img/user/TryHackMe/THM_Images/7e85a53da796d0888ca58303277d0a6d.png)    

![Exported image](/img/user/TryHackMe/THM_Images/8ec0d1139b73ebb1592dd8e6465ff1cf.png) 
Need to quarantine those who have not executed the file

![Exported image](/img/user/TryHackMe/THM_Images/fb997354cc4a73ecc2308b1fb9b2d617.png)  

Can now investigate the host who executed the file

![Exported image](/img/user/TryHackMe/THM_Images/93e70fa77726c90928b020c42d948562.png)  

![Exported image](/img/user/TryHackMe/THM_Images/51b3dc0baaf922690d1262cd396c015a.png)  

![Exported image](/img/user/TryHackMe/THM_Images/00b07cfe4909791b68ccd5bd5583f7c2.png)  

Can view what threat vector was used in order to continue

![Exported image](/img/user/TryHackMe/THM_Images/bc7868fe6ee06bcaa43d53ae9a8a4003.png)  

Once done analyzing the timeline, we can finish the case, giving us the flag.

![Exported image](/img/user/TryHackMe/THM_Images/c7066b4a5ec1333e8a6d096ae1f2e8f4.png)  

> [!Question]
> **What was the name of the malicious email sender?** 

> [!Success] Answer
> Jeff Johnson

> [!Question]
> **What was the threat vector?** 

> [!Success] Answer
> Email Attachment

> [!Question]
>  **How many devices downloaded the email attachment?** 

> [!Success] Answer
> 3

> [!Question]
> **How many devices executed the file?** 

> [!Success] Answer 
> 1

> [!Question]
> **What is the flag found at the end of the exercise?** 

> [!Success] Answer
> THM{My_First_Incident_Response}
