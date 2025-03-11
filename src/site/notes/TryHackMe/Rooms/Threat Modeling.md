---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/threat-modeling/","created":"2025-02-08T19:46:17.186-05:00","updated":"2025-03-11T00:32:59.424-04:00"}
---

# Task 2 - Threat Modeling Overview

- Threat modeling
	- Systematic approach to identifying, prioritizing, and addressing potential security issues
	- Develops proactive security measures and make informed decisions about resource allocation
	- Reduces risk exposure by identifying vulnerabilities and attack vectors

| **Type**          | **Definition**                                                                                                                                                               |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Threat**        | Refers to any potential occurrence, event, or actor that may exploit vulnerabilities to compromise information confidentiality, integrity, or availability.                  |
| **Vulnerability** | A weakness or flaw in a system, application, or process that may be exploited by a threat to cause harm. It may arise from software bugs, misconfiguration, or design flaws. |
| **Risk**          | The possibility of being compromised because of a threat taking advantage of a vulnerability. How likely an attack might be successful and how much damage it could cause.   |

- **High-level process of threat modeling**
	- **Defining the scope**
		- Identify the specific systems, applications, and networks
	- **Asset** **Identification**
		- Diagrams of the organization's architecture and its dependencies. 
		- Identify the importance of each asset based on the information it handles
	- **Identify Threats**
		- Identify potential threats that may impact the identified assets
	- **Analyze Vulnerabilities and Prioritize Risks** 
		- Analyze the vulnerabilities based on the potential impact of identified threats in conjunction with assessing the existing security controls. 
		- Risks should be prioritized based on their likelihood and impact.
	- **Develop and Implement Countermeasures**
		- Design and implement security controls to address the identified risks
	- **Monitor and Evaluate**
		- Continuously test and monitor the effectiveness of the implemented countermeasures and evaluate success
- **Attack tree**
	- Describes and analyzes potential threats again a system/app/infrastructure
	- Structured, hierarchical approach to breaking attacks into smaller components
	- Root node is attackers goal, other nodes represents events or conditions to reach goal
	- Attack path
		- Chain of vulnerabilities that are interconnected![](/img/user/TryHackMe/THM_Images/aaac5b89e9311f4d7ac6b4c2c667cbc6.png)

> [!Question] 
> **What is a weakness or flaw in a system, application, or process that can be exploited by a threat?**

> [!done] Answer
> Vulnerability

> [!Question]
> **Based on the provided high-level methodology, what is the process of developing diagrams to visualise the organisation's architecture and dependencies?**

> [!done] Answer
> Asset Identification

> [!Question] 
> **What diagram describes and analyses potential threats against a system or application?**

> [!done] Answer
> Attack Tree

# Task 3 - Modeling with MITRE ATT&CK

- MITRE ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge)
	- Comprehensive knowledge base of cyber adversary behavior and tactics
	- Shows different stages of cyber attacks and helps develop effective defense
	- Organized into a matrix that covers high-level objectives (tactics) and techniques
- Can be mapped into identified threats and vulnerabilities from threat modeling process
- Can be used for various purposes like
	- Identifying potential attack paths based on infrastructure
	- Developing threat scenarios
	- Prioritize vulnerability remediation

> [!Question] 
> **What is the technique ID of "Exploit Public-Facing Application"?**

![](/img/user/TryHackMe/THM_Images/f4f99e05daf5370d2178a22b1b828f25.png)

> [!done] Answer
> T1190

> [!Question] 
> **Under what tactic does this technique belong?**

Refer to screenshot above

> [!done] Answer
> Initial Access

# Task 4 - Mapping with ATT&CK Navigator

- Can use [ATTACK Navigator](https://mitre-attack.github.io/attack-navigator/) to navigate through the MITRE ATT&CK framework
	- Can create custom matrices that apply to their specific needs
- Overview of features
	- Creation of a new layer.
	- Searching and selecting techniques.
	- Viewing, sorting and filtering layers.
	- Annotating techniques with fills, scores and comments.


> [!Question] 
> **How many MITRE ATT&CK techniques are attributed to APT33?**

![](/img/user/TryHackMe/THM_Images/ff418537afb831e0580652e9420080ad.png)

> [!done] Answer
> 31

> [!Question] 
> **Upon applying the IaaS platform filter, how many techniques are under the Discovery tactic?**

![](/img/user/TryHackMe/THM_Images/f5c5419f26bb79e51623337e8e16303d.png)

> [!done] Answer
> 13

# DREAD Framework

Risk assessment tool by Microsoft to evaluate/prioritize threats and vulnerabilities

| **DREAD**           | **Definition**                                                                                                                                                                                                                              |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Damage**          | Data loss, system downtime, or reputational damage.                                                                                                                                                                                         |
| **Reproducibility** | The ease with which an attacker can successfully recreate the exploitation of a vulnerability.                                                                                                                                              |
| **Exploitability**  | The difficulty level involved in exploiting the vulnerability considering factors such as technical skills required, availability of tools or exploits.<br>Amount of time it would take to exploit the vulnerability successfully.          |
| **Affected Users**  | The number or portion of users impacted once the vulnerability has been exploited.                                                                                                                                                          |
| **Discoverability** | The ease with which an attacker can find and identify the vulnerability considering whether it is publicly known or how difficult it is to discover based on the exposure of the assets (publicly reachable or in a regulated environment). |

- Opinion-based model that heavily relies on an analyst's interpretation and assessment. 
- However, the reliability of this framework can still be improved by following some **guidelines**:
	- Establish a standardized set of guidelines and definitions for each DREAD category that provides a consistent understanding of how to rate vulnerabilities. 
		- Can be supported by providing examples and scenarios to illustrate how scores should be assigned under various circumstances.
	- Encourage collaboration and discussion among multiple teams. 
		- Constructive feedback from different members aids in justifying the assigned scores, which can lead to a more accurate assessment.
	- Use the DREAD framework with other risk-assessment methodologies and regularly review and update the chosen methods and techniques
		- Ensure they remain relevant and aligned with the organization's needs.
- **Qualitative Analysis using DREAD**
	- Rating each category from one to ten based on a subjective assessment and interpretation of the questions above. 
	- Average score of all criteria will calculate the overall DREAD risk rating. 


> [!Question] 
> **What DREAD component assesses the potential harm from successfully exploiting a vulnerability?**

> [!done] Answer
> Damage

> [!Question] 
> **What DREAD component evaluates how others can easily find and identify the vulnerability?**

> [!done] Answer
> Discoverability

> [!Question] 
> **Which DREAD component considers the number of impacted users when a vulnerability is exploited?**

> [!done] Answer
> Affected Users

# STRIDE Framework

Threat modelling methodology built upon the CIA Triad which helps identify and categories potential security threats in software development and system design.

| **Category**               | **Definition**                                                                                     | **Policy Violated** |
| -------------------------- | -------------------------------------------------------------------------------------------------- | ------------------- |
| **Spoofing**               | Unauthorised access or impersonation of a user or system.                                          | Authentication      |
| **Tampering**              | Unauthorised modification or manipulation of data or code.                                         | Integrity           |
| **Repudiation**            | Ability to deny having acted, typically due to insufficient auditing or logging.                   | Non-repudiation     |
| **Information Disclosure** | Unauthorised access to sensitive information, such as personal or financial data.                  | Confidentiality     |
| **Denial of Service**      | Disruption of the system's availability, preventing legitimate users from accessing it.            | Availability        |
| **Elevation of Privilege** | Unauthorised elevation of access privileges, allowing threat actors to perform unintended actions. | Authorisation       |

Representation of results for STRIDE framework is in a checklist table, one threat can cover multiple STRIDE components.

| **Scenario**                                                                                          | **Spoofing** | **Tampering** | **Repudiation** | **Information Disclosure** | **Denial of Service** | **Elevation of Privilege** |
| ----------------------------------------------------------------------------------------------------- | ------------ | ------------- | --------------- | -------------------------- | --------------------- | -------------------------- |
| **Sending a spoofed email, wherein the mail gateway lacks email security and logging configuration.** | ✔            |               | ✔               |                            |                       |                            |
| **Abusing an SQL injection vulnerability.**                                                           |              | ✔             |                 | ✔                          |                       |                            |

- **Threat Modeling with STRIDE:**
	- System Decomposition
		- Break down all accounted systems into components, such as applications, networks, and data flows. 
		- Understand the architecture, trust boundaries, and potential attack surfaces.
	- Apply STRIDE Categories
		- For each component, analyze its exposure to the six STRIDE threat categories. 
		- Identify potential threats and vulnerabilities related to each category.
	- Threat Assessment
		- Evaluate impact and likelihood of each identified threat. 
		- Consider potential consequences, ease of exploitation, and prioritize threats based on their overall risk level.
	- Develop Countermeasures 
		- Design and implement security controls to address the identified threats tailored to each STRIDE category.
	- Validation and Verification  
		- Test the effectiveness of the implemented countermeasures to ensure they effectively mitigate the identified threats.
	- Continuous Improvement  
		- Regularly review and update the threat model as the system evolves and new threats emerge.



> [!Question] 
> **What foundational information security concept does the STRIDE framework build upon?**

> [!done] Answer
> CIA Triad

> [!Question] 
> **What policy does Information Disclosure violate?**

> [!done] Answer
> Confidentiality

> [!Question] 
> **Which STRIDE component involves unauthorised modification or manipulation of data?**

> [!done] Answer
> Tampering

> [!Question] 
> **Which STRIDE component refers to the disruption of the system's availability?**

> [!done] Answer
> Denial of Service

> [!Question] 
> **Provide the flag for the simulated threat modelling exercise.**

Questions based off the following scenario,

Scenario: Your e-commerce company is in the process of designing a new payment processing system. To ensure its security and minimize the risk of compromise, you are tasked to conduct a threat modelling exercise using the STRIDE framework. All your assets are stored in a secure cloud infrastructure developed by your system architects.

As the leader of this initiative, you will be working with different teams to create a thorough threat modelling plan. Together, you aim to identify potential security threats and protect your payment processing system, ensuring the safety of your customers' information.

As a guide, here are the roles and responsibilities of the teams joining the initiative:

| **Team**                        | **Roles and Responsibilities**                                                                                                                          |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Development Team**            | Responsible for building systems and applications used by the organisation.                                                                             |
| **System Architecture Team**    | Responsible for designing the overall architecture of the cloud services used by the organisation.                                                      |
| **Security Team**               | Provide expertise on threats, vulnerabilities, and risk mitigation strategies.                                                                          |
| **Business Stakeholder Team**   | Provides valuable input on critical assets and business processes, and ensures alignment between the initiative and the organisation's strategic goals. |
| **Network Infrastructure Team** | Manages the organisation's network infrastructure, including servers and critical systems.                                                              |

![](/img/user/TryHackMe/THM_Images/569cd0cea1a77edf85b08324aaaab54a.png)


> [!done] Answer
> THM{m0d3ll1ng_w1th_STR1D3}

# PASTA Framework

﻿- Process for Attack Simulation and Threat Analysis
﻿- Structured, risk-centric threat modelling framework designed to help organizations identify and evaluate security threats and vulnerabilities within their systems, applications, or infrastructure. 
	﻿- Seven-step process that enables security teams to understand potential attack scenarios better, assess the likelihood and impact of threats, and prioritize remediation efforts accordingly.
 - Can be tailored to the organizations needs, meets compliance requirements

| **Define the Objectives**                   | Set clear and realistic security objectives for the threat modelling exercise. Identify relevant compliance requirements and industry-specific security standards.                                                                                                                  |
| ------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Define the Technical Scope**              | - Identify all critical assets, such as systems and applications, that handle sensitive data owned by the organization. Develop a thorough understanding of the system architecture, including data flows and dependencies.                                                         |
| **Decompose the Application**               | - Break down the system into manageable components or modules. Identify and document each component's possible entry points, trust boundaries, attack surfaces, data flows, and user flows.                                                                                         |
| **Analyse the Threats**                     | - Research and list potential threats from various sources, such as external attackers, insider threats, and accidental exposures. Leverage threat intelligence feeds and industry best practices to stay updated on emerging threats.                                              |
| **Vulnerabilities and Weaknesses Analysis** | - Use a combination of tools and techniques, such as static and dynamic code analysis, vulnerability scanning, and penetration testing, to identify potential weaknesses in the system. Keep track of known vulnerabilities and ensure they are addressed promptly.                 |
| **Analyse the Attacks**                     | - Develop realistic attack scenarios and simulate them to evaluate their potential consequences. Create a blueprint of scenarios via Attack Trees and ensure that all use cases are covered and aligned with the objective of the exercise.                                         |
| **Risk and Impact Analysis**                | - Assess the likelihood and impact of each identified threat and prioritize risks based on their overall severity. Determine the most effective and cost-efficient countermeasures for the identified risks, considering the organisation's risk tolerance and security objectives. |

> [!Question] 
> **In which step of the framework do you break down the system into its components?**

> [!done] Answer
> Decompose the application

> [!Question] 
> **During which step of the PASTA framework do you simulate potential attack scenarios?**

> [!done] Answer
> Analyze the attacks

> [!Question] 
> **In which step of the PASTA framework do you create an inventory of assets?**

> [!done] Answer
> Define the technical scope

> [!Question] 
> **Provide the flag for the simulated threat modelling exercise.**

Scenario: Your organization is known for its online banking platform, catering to many users across the Asia Pacific region. To ensure its resiliency to potential threats, you are tasked to conduct a threat modelling exercise using the PASTA framework.

As the leader of this initiative, you will be working with different teams to create a thorough threat modelling plan. Together, you aim to identify potential security threats and protect your online banking platform, ensuring the safety of your customers' information.

As a guide, here are the roles and responsibilities of the teams joining the initiative:

|   |   |
|---|---|
|**Team**|**Roles and Responsibilities**|
|**Development Team**|Responsible for building systems and applications used by the organisation.|
|**System Architecture Team**|Responsible for designing the overall architecture of the cloud services used by the organisation.|
|**Security Team**|Provide expertise on threats, vulnerabilities, and risk mitigation strategies.|
|**Business Stakeholder Team**|Provides valuable input on critical assets and business processes, and ensures alignment between the initiative and the organisation's strategic goals.|

You must follow the seven-step PASTA process in choosing whom to approach for the information you need for this threat modelling exercise.

![](/img/user/TryHackMe/THM_Images/145530eadb2158ef8a0b9b5d7073b075.png)

> [!done] Answer
> THM{c00k1ng_thr34ts_w_P4ST4}
# Summary

| Framework        | Use Case Applications                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **MITRE ATT&CK** | Unlike DREAD and STRIDE, which focus more on potential risks and vulnerabilities, ATT&CK provides a practical and hands-on approach by mapping adversary tactics. Assess the effectiveness of existing controls against known attack techniques used by threat actors.                                                                                                                                                                                          |
| **DREAD**        | DREAD offers a more numerical and calculated approach to threat analysis than STRIDE or MITRE ATT&CK, making it excellent for clearly prioritising threats. Qualitatively assess the potential risks associated with specific threats. Prioritise risk mitigation based on the collective score produced by each DREAD component.                                                                                                                               |
| **STRIDE**       | While other frameworks like MITRE ATT&CK focus on real-world adversary tactics, STRIDE shines in its structure and methodology, allowing for a systematic review of threats specific to software systems. Analyse and categorise threats in software systems.<br>- Identify potential vulnerabilities in system components based on the six STRIDE threat categories. Implement appropriate security controls to mitigate specific threat types.                |
| **PASTA**        | Excellent for aligning threat modelling with business objectives. Unlike other frameworks, PASTA integrates business context, making it a more holistic and adaptable choice for organisations. Conduct risk-centric threat modelling exercises aligned with business objectives. Prioritise threats based on their potential impact and risk level to the organisation. Build a flexible methodology that can be adapted to different organisational contexts. |
