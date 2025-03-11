---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/ssdlc/","created":"2025-02-23T21:15:28.539-05:00","updated":"2025-03-11T00:32:59.406-04:00"}
---

# Task 2 - What is SSDLC?

- **Secure Software Development Lifecycle (SSDLC)**  
	- During SDLC, security testing was introduced very late in the lifecycle. ﻿
		- Bugs, flaws, and other vulnerabilities were identified late, far more expensive and time-consuming to fix.
		- Not considered during the testing phase
			- End-users reported bugs after deployment. 
		- Secure SDLC models aim to introduce security at every stage of the SDLC.  
- **Why is Secure SDLC important?**
	- IBM discovered that it costs six times more to fix a bug found during implementation than one identified during design phase. 
	- Costs 15 times more if flaws are identified during testing
	- Up to 100 times more costly if identified during the maintenance and operation phases
- **Benefits of SDLC**
	- Boosting security education and awareness: all stakeholders know each phase's security recommendations and requirements.
	- Flaws are detected early before deployment, reducing the risk of getting hacked or disrupted.
	- Costs are reduced, and speed increases, thanks to the early detection and resolution of vulnerabilities.
	- Business risk, brand reputation damage, and fines that could lead to economic disaster for a company are prevented.

> [!Question]
>  **How much more does it cost to identify vulnerabilities during the testing phase?**

> [!Success] Answer
> 15

# Task 3 - Implementing SSDLC

- **Understanding Security Posture**
	- Understanding gaps and state is critical for successfully introducing a new tool, solution, or change.
	- **Gap analysis** 
		- Determines what activities and policies exist in your organization and how effective they are.
	- **Software Security Initiatives** **(SSI)**
		- Establish realistic and achievable goals with defined metrics for success. 
		- **Formalize processes for security activities**  
			- Essential to spend time helping engineers get familiarized with a new process and gather feedback before enforcing it. 
			- During gap analysis, every policy should have defined procedures to make them effective.  
	- **Invest in security training** 
		- For engineers as well as appropriate tools. 
		- Ensure people are aware of new processes and the tools that will come with them to operationalize them
- **SSDLC Processes**
	- **Risk Assessment (Planning & Requirements)**
		- Identify security considerations that promote a security by design approach when functional requirements are gathered
	- **Threat Modeling (Design and Prototyping)**
		- Process of identifying potential threats when there is a lack of appropriate safeguards. 
		- Focuses on what should not happen. 
			- In contrast, design requirements state how the software will behave and interact.
	- **Code Scanning/Review (Software Development)**
		- Either manual or automated. 
		- Can leverage Static and Dynamic Security testing technologies
	- **Security Assessments (Operations and Maintenance)**
		- Penetration Testing & Vulnerability Assessments 
			- Form of automated testing that can identify critical paths of an application that may lead to exploitation of a vulnerability. 
		- Carried out during the Operations & Maintenance phase of the SDLC after a prototype of the application.

> [!Question]
>  **What should you understand before implementing Secure SDLC processes?**

> [!Success] Answer
> Security Posture

> [!Question]
>  **During which stages should you perform a Risk Assessment?**

> [!Success] Answer
> Planning and Requirements

> [!Question]
>  **What should be carried out during the design phase?**

> [!Success] Answer
> Threat Modeling
# Task 4 - Risk Assessment

- **Risk** refers to the likelihood of a threat being exploited, negatively impacting a resource or the target it affects.
- **Risk management** is an important pillar to integrate into the SDLC to mitigate risk in a product or service.
- **Risk assessment** 
	- Determines the level of a potential threat. 
	- Risk identified can be reduced or eliminated by applying appropriate controls during the risk mitigation process. 
	- Followed by threat modelling
- **Performing a risk assessment**
	- **Assume the software will be attacked** and consider the factors that motivate the threat actor. 
		- Factors such as the data value of the program, companies security level, clients, and software distribution (single, small workgroup or released worldwide). 
			- Write down the acceptable level of risk for each of them.
			- Company and other stakeholders have to decide whether it is worth it
				- it is also crucial to communicate these tradeoffs. 
	- **Risk evaluation** 
		- Include factors like the worst-case scenario if the attacker has successfully attacked the software. 
			- Determine value of data like user's identity, credentials access, or assets
			- Determine complexity of attack
			- The high level of risk will not be acceptable
				- Best to mitigate it
			- Users affected are a vital factor.
			- Determine accessibility of the target. 
				- Determine whether the target accepts requests across a network or only local access. 
					- More impact if an attacker accesses a production environment vs a sandbox environment
- **Types of Risk Assessments**
	- **Qualitative Risk Assessment**
		- Most common 
		- Goal is to assess and classify risk into thresholds like "Low", "Medium", and "High". 
		- Examines what can cause harm and what decisions should be made to define or improve adequate control measures. 
		- `Risk = Severity x Likelihood`	
			- "Severity" is the impact of the consequence
			- Likelihood is the probability of it happening.
	- **Quantitative Risk Assessment**  
		- Used to measure risk with numerical values.
		- Can use tools to determine Severity and Likelihood or calculate based on the company's processes.
		- Vital to understand a security posture and its processes in order to properly assign value
- **Example**
	- "Customer data gets exfiltrated by an attack". 
	- Once the system is developed, you can perform quantitative risk analysis
		- "One customer can sue us for $ 20,000 if their data gets leaked", and we have 100 customers. 
		- However, the Annual Rate of Occurrence (ARO) is 0.001. 
			- Hence Annual Loss Expectancy is = $20,000 * 100 * 0.001 = $ 2,000, 
		- As long as our compensating security control is less than $ 2,000, we are not overspending on security.

> [!Question]
>  **What is a formula to assign a Qualitative Risk level?**

> [!Success] Answer
> Severity x Likelihood

> [!Question]
>  **Which type of Risk Assessment assigns numerical values to determine risk?**

> [!Success] Answer
> Quantitative Risk Assessment
# Task 5 - Threat Modeling 

Information based on  [Threat Modeling](Threat%20Modeling.md)

> [!Question]
>  **What threat modelling methodology assigns a rating system based on risk probability?**

> [!Success] Answer
> DREAD

> [!Question]
>  **What threat modelling methodology is built upon the CIA triad?**

> [!Success] Answer
> STRIDE

> [!Question]
>  **What threat modelling methodology helps align technical requirements with business objectives?**

> [!Success] Answer
> PASTA

# Task 6 - Secure Coding

- **Secure code review & analysis**
	- Implementing a secure code review in the phases of an SDLC, will increase the resilience and security of the product without bearing any additional cost for future patches
		- Defined as a measure where the code itself is verified and validated to ensure vulnerabilities that are found can be mitigated and removed 
	- Having aware developers and be proactive in reviewing the code during development
		- Prevents any setbacks on the release and issues exposed to the users.
	- Demonstrates compliance with standards
- **Code review** 
	- **Manual code review**
		- Expert analyses and checks the source code by going line by line to identify vulnerabilities. 
		- Requires them to communicate with the software developers to get hold of the purpose and functionalities of the application.
		- Output will then be reported to the developers if there is a need for bug fixing.
	- Can be automated as well
- **Code Analysis**
	- **Static Analysis** 
		- Examines the source code without executing the program.
		- Detects bugs at the implementation level
	- **Dynamic analysis**
		- Looks at the source code when the program is running
		- Detects errors during program runtime. 
	- **SAST (Static Application Security Testing)**
		- **White box testing method** that directly analyses the source code. 
		- Is done before an application is live and running
		- Can even help detect vulnerabilities in your application during the SDLC development phases.
		- Uses a testing methodology of **analyzing a source code to detect any traces of vulnerabilities** 
			- Analyses and scans an application before the code is compiled. 
			- Once a vulnerability is detected, the following line of action is to check the code and patch the code before the code is compiled and deployed to live. 
			- Test software's inner structure and see how it integrates with the external systems.
		- **Software Composition Analysis (SCA)**
			- Used to scan dependencies for security vulnerabilities, 
				- Helps development teams track and analyze any open-source component brought into a project. 
			- Essential in security testing as modern applications are increasingly composed of open-source code. 
			- Biggest challenges developer teams have is ensuring their codebase is secure as applications are assembled from different building blocks.
	- **DAST (Dynamic Application Security Testing)**
		- **Black-box testing method** that finds vulnerabilities at runtime. 
		- Tool to scan any web application to find security vulnerabilities. 
			- Used to detect vulnerabilities applications that are deployed in production. 
			- Sends alerts for remediation.
		- **Works by simulating automated attacks on an application**, mimicking a malicious attacker. 
			- Goal is to find unexpected outcomes or results that attackers could use to compromise an application. 
			- Don't have internal information about the application or the source code
		- Can be integrated very early into the software development lifecycle. 
			- Helps organizations reduce and protect against the risk that application vulnerabilities could cause. 
			- Typically used during the testing phase of SDLC.
	- **IAST (Interactive Application Security Testing)**
		- Analyses code for security vulnerabilities while the app is running. 
			- Deployed side by side with the main application on the application server. 
		- Application security tool designed for web and mobile applications to detect and report issues even while running.
		- Uses the **Grey Box Testing Methodology**.
			- Occurs in real-time while the application runs in the staging environment. 
			- Can identify the line of code causing security issues and quickly inform the developer for immediate remediation.
			- IAST agents are deployed on the application servers. 
				- When DAST scanner reports a vulnerability, the deployed IAST agent will then return a line number of the issue from the source code. 
				- During functional testing performed by a QA tester, the agent studies every pattern that a data transfer inside the application
	- **RASP (Runtime Application Self Protection)** 
		- Application integrated into an application to **analyze inward and outward traffic and end-user behavioral patterns** 
		- Used after product release
			- More security-focused tool than testing.
		- **Deployed to a web or application server next to the main application while running.** 
			- Send alerts to the security team and immediately block access to the individual making a malicious request. 
			- Secures the application against different attacks. 
				- Does not just wait or try to rely only on specific signatures of some known vulnerabilities.

> [!Question]
>  **Is it recommended to use SAST analysis at the beginning of the SDLC? (y/n)**

> [!Success] Answer
> Y

> [!Question]
>  **Which type of code analysis uses the black-box method?**

> [!Success] Answer
> DAST

> [!Question]
>  **Which type of code analysis uses the white-box method?**

> [!Success] Answer
> SAST
# Task 7 - Security Assessments

Information based of this [Vulnerability Management](Vulnerability%20Management.md)

**Vulnerability Assessment** 

| Pros                                                         | Cons                                                                                                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| - Suitable for quickly identifying potential vulnerabilities | - Can produce a large number of reports                                                                                                           |
| - Part of the Penetration Test                               | - Quality depends on the tool used                                                                                                                |
| - Better for Budget, they are cheaper than Pentests          | - Real-life scenarios for vulnerabilities are not considered (it could be behind a proxy or only exploitable with social engineering/credentials) |
|                                                              | - The low-risk vulnerability may be used as part of a more powerful attack.                                                                       |

**Penetration Testing**

| Pros                                                                          | Cons                                                        |
| ----------------------------------------------------------------------------- | ----------------------------------------------------------- |
| Tester shows organisations what an attacker could do.                         | Very Expensive                                              |
| How any vulnerabilities could be used against it by attackers – the real risk | Requires extensive planning and time to carry out the tests |
| Can be shown to the customer                                                  |                                                             |

> [!Question]
>  **Which form of assessment is more budget-friendly and takes less time?**

> [!Success] Answer
> Vulnerability Assessment

> [!Question]
>  **Which type of assessment identifies vulnerabilities and attempts to exploit them?**

> [!Success] Answer
> Penetration Testing

> [!Question]
>  **When do you typically carry out Vulnerability Assessments or Pentests?**

> [!Success] Answer
> Operations & Maintenance

# Task 8 - SSDLC Methodologies

- **Microsoft's Security Development Lifecycle (SDL)**
	- **Collection of mandatory security activities** grouped by the traditional software development lifecycle phases.
		- Heavy emphasis on understanding the cause and effect of security vulnerabilities
			- Data is collected to assess training effectiveness. 
			- In-process metrics are used to confirm process compliance. 
			- Post-release metrics are used to guide future changes.
	- Secure by **Design**
		- Security is a built-in quality attribute affecting the whole software lifecycle.
	- Security by **Default**
		- Software systems are constructed to minimize potential harm caused by attackers, 
		- e.g. software is deployed with the least necessary privilege.
	- Secure in **Deployment**
		- Software deployment is accompanied by tools and guidance supporting users and administrators.
	- **Communications**
		- Software developers are prepared for occurring threats by communicating openly and timely with users and administrators
- **OWASP Secure Software Development Life Cycle Project (S-SDLC)**
	- Aims to build "security quality gates", to support quality and secure software made throughout the pipeline. 
	- Follows Agile Security approach, where sprints are dedicated to security. 
		- Code reviews, authentication, authorization, input validation, and assessing technical risks like code injections. 
	- Based on a "Maturity Model" approach with OWASP SAMM.
	- **Software Assurance Maturity Model (SAMM)** 
		- Open framework to formulate and implement a software security strategy tailored to the organization's specific risks. 
		- Evaluates an organization's existing software security practices
			- Builds a software security assurance program 
			- Defines and measures security activities
		- Helps explain objectives, actions, results, success metrics, costs etc
- **Building Security In Maturity Model (BSIMM)**
	- Study of real-world software security initiatives, reflects the current state of software security.
	- "Measuring stick" to understand your security posture by providing a comparison of other companies' security states. 
	- Tells you what your doing wrong 
- **Software Security Touchpoints**

> [!Question]
>  **What methodology follows a set of mandatory procedures embedded in the SDLC?**

> [!Success] Answer
> Microsoft SDL

> [!Question]
>  **What Maturity Model helps you measure tailored risks facing your organisation?**

> [!Success] Answer
> SAMM

> [!Question]
>  **What maturity model acts as a measuring stick to determine your security posture?**

> [!Success] Answer
> BSIMM
# Task 9 - Secure Space Lifecycle 

Complete the challenge to get the flag

![](/img/user/TryHackMe/THM_Images/408415fd0334eef58931924de3513eaa.png)

![](/img/user/TryHackMe/THM_Images/6c5affde7fae0a0804756452e792aff4.png)

> [!Question]
>  **What is the flag?**

> [!Success] Answer
> THM{D0-A-Barr3l-R011}

