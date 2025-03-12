---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/introduction-to-dev-sec-ops/","created":"2025-03-11T17:50:01.905-04:00","updated":"2025-03-12T00:21:28.339-04:00"}
---

# Task 2 - DevOps: A New Hope

- **Waterfall Model**
	- Constituted and relied on a hierarchy, where every member had a specific responsibility. 
		- System admins kept everything running smoothly 
		- Developers build features 
		- QA engineers test the system's functionality
	- But what if there is a flaw? A bug? Who fixes it? 
		- Led to blame games and passing the baton around that created friction, loads of backlog, not efficient at all
- **Agile Model**
	- Emphasizing four values for agile development:
		- Individuals and interactions over processes and tools
		- Working software over comprehensive documentation
		- Customer collaboration over contract negotiation
		- Responding to change vs following a plan
		- Emphasis on team collaboration and self-organizing teams, plenty of room for change and flexibility.
- **DevOps**
	- Focuses on driving **cultural change** to increase efficiency 
		- Units the magic of all teams working on a project, using integration and automation.
		- Cross-integration across all departments, QA+sysadmins+developers
			- Developers can now be involved in deployment and sysadmins can now write scripts
			- QA can figure out how to fix flaws vs constantly testing for functionality
			- Through automation and integration of systems, engineers can now have the same visibility at all times and interact accordingly
- **DevOps Importance**
	- Emphasizes building trust and better liaising between teams
	- Aligns technological projects to business requirements, projects become more efficient and prioritized accordingly.
	- Small and reversible changes, visible to all teams involved.
		- Better contribution and communication
- **Summary**
	- Developers can provide resources to public clouds without depending on IT to provision infrastructure
	- CI/CD processes automatically set up testing, staging, and production environments. 
		- Decommissioned, scaled, or re-configured as needed.
	- IaC is widely used to deploy environments **declaratively***, using tools like Terraform and Vagrant.
		- Declarative approach requires that users **specify the end state** of the infrastructure
			- For example, deploy machines in a running state directly into an environment, automating the configuration choices throughout the workflow. 
			- The software builds it and releases it with no human interaction
	- Organizations can now provision containerized workloads dynamically using automated, adaptive processes


> [!Question]
>  **What methodology relies on self-organising teams that focus on constructive collaboration?**

> [!Success] Answer
> Agile

> [!Question]
>  **What methodology relies on automation and integration to drive cultural change and unite teams?**

> [!Success] Answer
> DevOps

> [!Question]
>  **What traditional approach to project management led to mistrust and poor communication between development teams?**

> [!Success] Answer
> Waterfall

> [!Question]
>  **What does DevOps emphasize?**

> [!Success] Answer
> Building trust

# Task 3 - The Infinite Loop

![500](/img/user/TryHackMe/THM_Images/5725a6cb08d041826239b13181de1f77.png)

- **Tools and Processes** 
	- **CI/ CD**
		- Deals with the frequent merging of code and adding testing in an automated manner to perform checks as new code is pushed and merged.
		- Test code as we push and merge thanks minor code changes systematically and routinely. 
		- Detects bugs early and decreases the effort of maintaining modular code massively, which introduces reliable rollbacks of versions/code.
	- **INFRASTRUCTURE AS CODE** **(IaC)**
		- Manage and provision infrastructure through code and automation. 
			- Can reuse code used to deploy infrastructure, helps inconsistent resource creation and management. 
		- Standard tools are terraform, vagrant, etc.
	- **CONFIGURATION MANAGEMENT**
		- State of infrastructure is managed constantly and applying changes efficiently, making it more maintainable. 
		- Visibility into how infrastructure is configured
	- **ORCHESTRATION**
		- Automation of workflows, helps achieve stability
		- For example, can have fast responses whenever there is a problem (e.g., health checks failing);
	- **MONITORING**
		- Focuses on collecting data about the performance and stability of services and infrastructure. 
		- Faster recovery, helps with cross-team visibility, provides more data to analyze for better root-cause analysis
		- Generates an automated response
	- **MICROSERVICES**
		- Breaks an application into many small services.
		- Flexibility if there is a need to scale, reduced complexity, and more options for choosing technology across microservices.

> [!Question]
>  **What helps in adding tests in an automated manner and deals with the frequent merging of small code changes?**

> [!Success] Answer
> CI/CD

> [!Question]
>  **What process focuses on collecting data to analyse the performance and stability of services?**

> [!Success] Answer
> Monitoring

> [!Question]
>  **What is a way to provision infrastructure through reusable and consistent pieces of code?**

> [!Success] Answer
> IaC

# Task 4 - Shifting Left

- Security can be easily integrated due to the visibility and flexibility of DevOps
	- Risks are reduced massively 
	- Integrating code analysis tools and automated tests earlier in the process can now identify security flaws during early development.
- **Shifting Left**
	- Focus on **instilling security from the earliest stages** in the development lifecycle and introducing a more collaborative culture between development and security.
	- Implementing security measures during all stages of the development lifecycle rather than at the end of the cycle will ensure the software is designed with security best practices built in.
	- By detecting security flaws early in development
		- remediation costs are lower
		- No need to roll back changes as they are being addressed on time
		- Reduces cost, builds trust, and improves the security and quality of the product
- Provisioning of infrastructure in the cloud is now automated. 
	- Can also spark **security concerns and lead to flaws**
- Shift-Left approach ensures these flaws are caught early by introducing processes from the start. 
	- Post-development security reviews or cloud infrastructure configurations analysis become a bottleneck. 
	- Not enough time to remediate discovered problems before the next version or feature is introduced.
		- Need a fast-paced environment for scaling and growth to keep with customer needs. 
	- Security is at **risk** of being left behind
		- Instilling security in the beginning and adapting security testing to become flexible increases the chances of addressing things promptly.
- **DevSecOps**
	- Development approach to shifting left in DevOps
	- With DevOps, security gets to be introduced early in the development cycle and this minimizes risks massively. 
		- Integrating code analysis tools and automated tests earlier in the process can lead to better identification and elimination of security loopholes. And
		- Security is not an add-on. It's a must-have design feature. 
		- Enhances the impact of DevOps and eliminate a lot of other bottlenecks that could arise otherwise.

> [!Question]
>  **What term is it used to describe accounting for security from the earliest stages in a development lifecycle?**

> [!Success] Answer
> Shift left

> [!Question]
>  **What is the development approach where security is introduced from the early stages of a development lifecycle until the final stages?**

> [!Success] Answer
> Devsecops
# Task 5 - DevSecOps: Security Strikes Back

- DevSecOps relies on automation and platform design that integrates security as a shared responsibility. 
	- Culture-driven development style that normalizes security as a day-to-day operation.
- **Value**
	- Helps bring down vulnerabilities, maximizes test coverage, and intensifies the automation of security frameworks. 
	- Reduces risk massively, easier for auditing and monitoring.
- **Implementation**
	- Culture is key.  
		- It only works with collective effort. 
	- Should aim to bridge the security knowledge gaps between teams 
		- they all first need the tools and knowledge to drive this autonomy efficiently and confidently. 
- **Challenges**
	- **Security Silos**
		- Common for many security teams to only have specialized people that can only maintain and lead security practices. 
		- Creates a silo around security and prevents engineers from understanding the necessity of security or applying security measures from the beginning.
			- Not scalable or flexible. 
		- Security should be a supportive function to promote secure solutions and decisions.
			- Best practice is to share these responsibilities across all team members instead of having a specialized security engineer.
	- **Lack of Visibility & Prioritization**
		- Have a culture where security is treated as a regular aspect of the application. 
		- Developers can then focus on development with confidence about security instead of relying solely on security departments
		- Trust should be built between teams
	- **Stringent Processes**
		- Every new software must not go through a complicated process and verification against security compliances before being used by developers.
		- Procedures should be flexible 
			- Lower-level tasks should be treated differently
			- Higher-risk tasks and changes are targeted for these more stringent processes.
		- Developers need sandbox environments to test new software without common security limitations. 

> [!Question]
>  **What DevSecOps challenge can lead to a siloed culture?**

> [!Success] Answer
> Security Silos

> [!Question]
>  **What DevSecOps challenge can affect not prioritizing the right risks at the right times?**

> [!Success] Answer
> Lack of Visibility

> [!Question]
>  **What DevSecOps challenge stems from needlessly overcomplicated security processes?**

> [!Success] Answer
> Stringent Processes
# Task 6 - DevSecOps Culture

- **Promote autonomy of teams**
	- Automate processes that fit seamlessly with the development pipeline until security tests become just another type of test like unit testing
	- Leading by example and promoting education like creating playbooks / runbooks to spot these flaws and fix them
	- Understand their risk, and build confidence in engineers to make the secure decision independently
		- Security should act as a supporting function that focuses on building trust
		- Create as much overlap in knowledge between teams as possible.
- **Visibility and Transparency**
	- For every tool, there needs to be a supporting process that provides visibility and promotes transparency to other teams. 
	- Need to have **visibility** on the security state of the service they own or maintain.
	- For example
		- A dashboard visualizes the number of security flaws by the criticality of the service. 
		- Helps prioritize accordingly, can tackle flaws at the right time. 
	- **Transparency** 
		- Introducing tools and practices that are accessible to teams. 
		- For example, 
			- If you present a check before merging code and it fails, developer should have access to the tool that is flagging that message.
- **Account for flexibility thanks to understanding and empathy**
	﻿- Definition of risk for security teams is unequivocal, but for other teams, risk can be different and just as precise for them.
	﻿- Ramifies into what they prioritize, how they work, and when to leave project with a tight deadline to fix a bug.
	- There is no magic tool or process for everyone.
		- It is essential to understand how developers/engineers work, what they know to be a risk, and what they prioritize.
		- Easier to build a process that finds common ground and has a higher chance to work vs adding another tool that creates more stress for them. 

> [!Question]
>  **How can you make security scalable so it's not left behind when start ups face hypergrowth or in large corporations?**

> [!Success] Answer
> Promote autonomy of teams

> [!Question]
>  **How can you support teams in understanding risk and educating on security flaws?**

> [!Success] Answer
> Visibility and Transparency

> [!Question]
>  **What are key factors to successfully instill security in the development process by accounting for flexibility?**

> [!Success] Answer
> Understanding and Empathy

# Task 7 - Fuel Trouble

Go to the website given and go through each of the comics to answer the following questions

> [!Question]
>  **What Software Development Model did the team in Comic 1 follow?**

> [!Success] Answer
> Waterfall

> [!Question]
>  **What Software Development Model did the team in Comic 2 follow?**

> [!Success] Answer
> Agile

> [!Question]
>  **What Software Development Model did the team in Comic 3 follow?**

> [!Success] Answer
> DevOps

> [!Question]
>  **Question?**

![](/img/user/TryHackMe/THM_Images/52ad2c7131baab2ee6b55ba9753342fc.png)

> [!Success] Answer
> THM{ONE_TWO_THREE}
