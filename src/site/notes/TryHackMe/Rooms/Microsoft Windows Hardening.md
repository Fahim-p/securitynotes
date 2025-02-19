---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/microsoft-windows-hardening/","created":"2025-02-18T14:46:59.028-05:00","updated":"2025-02-18T22:27:15.211-05:00"}
---

# Task 2 - Understanding General Concepts

- **Windows Services**
	- Creates/manages critical functions such as network, storage, user credentials, etc. 
	- Runs automatically in the background. 
	- Managed by the **Service Control Manager** panel and divided into three categories
		- Local, Network & System
	- Type `services.msc` in the `Run` window
- **Windows Registry** 
	- Unified container database that stores configurational settings, essential keys and shared preferences for Windows and third-party applications. 
	- Uses a registry editor for storing various states of the application. 
		- For example, if an application wants to execute itself during the computer boot-up process; 
			- It will store its entry in the `Run` & `Run Once` key.
	- Malicious programs can make undesired changes in the registry editor and tries to abuse its program or service as part of system routine activities. 
		- Can protect the registry editor by limiting its access to unauthorized users.
	- Type `regedit` in the Run dialogue or taskbar search to access the registry editor.
- **Event Viewer**
	- Shows log details about all events occurring on your computer 
	- Receives notifications from different services and applications running on the computer
		- Stored in a centralized database.   
	- Hackers and malicious actors access it to increase their attack surface and enhance the target system's profiling. 
	- **Event categories**:
		- Application: Records events of already installed programs.
		- System: Records events of system components.
		- Security: Logs events related to security and authentication etc.
	- Can access it by typing `eventvwr` in the `Run` window. 
		- Default location for storing events is `C:\WINDOWS\system32\config\folder`
- **Telemetry**
	- Data collection system used by Microsoft to enhance the user experience
	- Preemptively identifies security and functional issues in software. 
	- Applications seamlessly shares data  
	- Achieved by **Universal Telemetry Client (UTC)** services available in Windows and runs through `diagtrack.dll`. 
	- Stored encrypted in a local folder `%ProgramData%\Microsoft\Diagnosis`


> [!Question]
> **What is the startup type of App Readiness service in the services panel?**

RDP'ed into the server using credentials, searched for `services`

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218164355.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218150718.png)

> [!done] Answer
> Manual

> [!Question]
> **Open Registry Editor and find the key “tryhackme”. What is the default value of the key?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218150808.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218150824.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218150913.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218150928.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218150945.png)

> [!done] Answer
> {THM_REG_FLAG}

> [!Question]
> **Open the Diagnosis folder and go through the various log files. Can you find the flag?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218151711.png)

Needed admin permissions to open "flag.txt.txt", so I opened `cmd` as administrator and opened the file through there.

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218152034.png)

> [!done] Answer
> {THM_1000710}

> [!Question]
> **Open the Event Viewer and play with various event viewer filters like Information, Error, Warning etc. Which error type has the maximum number of logs?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218152414.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218152352.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218152855.png)

> [!done] Answer
> Level: Error
# Task 3 - Identity & Access Management

- **Standard vs Admin Account** 
	- Identity and access management ensures that only authenticated and authorized users can access the system. 
	- There are two types of accounts in Windows 
		- Admin
			- Should only be used to carry out tasks like software installation and accessing the registry editor, service panel, etc. 
		- Standard Account. 
			- Used for routine functions like access to regular applications, including Microsoft Office, browser, etc.
	- Go to `Control Panel > User Accounts` to create standard or administrator accounts.
		- A user can authenticate themselves on the system through a **password**; 
			-  **Windows Hello**, allows authenticating someone based on other factors like "something you are". 
			- Go to `Settings > Accounts > Sign-in Options.`
- **User Account Control (UAC)**
	- Enforces enhanced access control and ensures that all services and applications execute in non-administrator accounts. 
		- Mitigates malware's impact and minimizes privilege escalation.
	- Actions requiring elevated privileges will ask for administrative credentials
		- For example, installing device drivers or allowing inbound connections through Windows Firewall 
	- Best practice is to follow the **Principle of Least Privilege**  
		- Can also keep the notification level to "Always Notify" in the UAC settings
	- Go to `Control Panel -> User Accounts` and click on `Change User Account Control Setting`.
- **Local Policy and Group Policies Editor**
	- Built-in interactive tool that allows to configure and implement local and group policies. 
	- Mainly used when apart of a network
		- Can also use it for a workstation to limit administrative permissions.
	- Not available in Windows Home but only in the Pro and Enterprise versions.
- **Password Policies**
	- We can design password policies to maximize our security
	- We can access Password policies through the Local group policy editor.
	- Go to `Security settings > Account Policies > Password policy`
- **Setting A Lockout Policy**
	- Can set out a lockout policy so the account will automatically lock after certain invalid attempts. 
	- Go to `Local Security Policy > Windows Settings > Account Policies > Account Lockout Policy`


> [!Question]
> **Find the name of the Administrator Account of the attached VM**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218160218.png)

> [!done] Answer
> Harden

> [!Question]
> **Go to the User Account Control Setting Panel (Control Panel > All Control Panel Items > User Accounts). What is the default level of Notification?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218160350.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218160421.png)

> [!done] Answer
> Always Notify

> [!Question]
> **How many standard accounts are created in the VM?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218160218.png)

Only one administrator account, no standard accounts

> [!done] Answer
> 0

# Task 4 - Network Management

- **Windows Defender Firewall**
	- Protects computers from malicious attacks and blocks unauthorized traffic through inbound and outbound rules or filters.
	- Malicious actors abuse Windows Firewall by bypassing existing rules.
		- For example, if we have configured the firewall to allow incoming connections, hackers will try to manipulate the functionality by creating a remote connection to the victim's computer.
	- We can access it through `WF.msc` in the Run dialogue.
	- Three main profiles `Domain, Public and Private`
		- Private profile must be activated with "Blocked Incoming Connections"
	- Whenever possible, use default settings. 
		- For blocking all the incoming traffic, always configure the firewall with a 'default deny' rule before making an exception rule that allows more specific traffic.
- **Disable unused Networking Devices**
	- Recommended to disable network interfaces so that threat actors cannot access them and use them for data retrieval from the victim's computer.  
	- Go to `Control panel > System and Security Setting > System > Device Manager` and disable all the unused Networking devices.
- **Disable SMB protocol**
	- File-sharing protocol exploited by hackers in the wild. 
	- Must disable the protocol if your computer is not part of a network by issuing the following command in PowerShell.
		- `Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol`
-  **Protecting Local Domain Name System (DNS)** 
	- Naming system that translates Fully Qualified Domain Names (FQDN) into IP addresses.
		- If the attacker places himself in the middle, he may intercept and manipulate DNS requests
		- Can point them to attacker-controlled systems since DNS replies are neither authenticated nor encrypted.  
	- The hosts file located in Windows acts like local DNS and is responsible for resolving hostnames to IP addresses. 
		- Malicious actors try to edit the file's content to reroute traffic to their command and control server.  
		- Located at `C:\Windows\System32\Drivers\etc\hosts`.
- **Mitigating Address Resolution Protocol (ARP) Attack**  
	- Resolves MAC addresses from given IP addresses saved in the workstations ARP cache. 
	- Offers no authentication and accepts responses from any user in the network. 
		- An attacker can flood target systems with crafted ARP responses
		- Can point to an attacker-controlled machine and put him in the middle of communication between the targeted hosts.
	- Use **`arp -a`** in cmd to check ARP entries.
		- Table contains MAC addresses in the middle and IP addresses in the left.  
		- If the table includes a MAC mapped to two IPs, you are probably susceptible to an ARP poisoning attack.
			- To clear the ARP cache and prevent the attack, issue the command `arp -d`.
- **Preventing Remote Access to Machine**  
	- Remote access provides a way to connect to other computers/networks even located at a different geographical location for file sharing and remotely make changes to a workstation. 
	- Microsoft has developed a Remote Desktop Protocol (RDP) for connecting with other computers. 
	- Can disable it through `settings > Remote Desktop`. 
		- Or `Update & Security > For Developers > Remote Desktop > Show Settings > Remote`

> [!Question]
> **Open Windows Firewall and click on Monitoring in the left pane - which of the following profiles is active? Domain, Private, Public?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218163838.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218163912.png)

> [!done] Answer
> Private

> [!Question]
> **Find the IP address resolved for the website tryhack.me in the Virtual Machine as per the local hosts file.**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218164159.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218164211.png)

> [!done] Answer
> 192.168.1.140 

> [!Question]
> **Open the command prompt and enter arp -a. What is the Physical address for the IP address 255.255.255.255?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218164253.png)

> [!done] Answer
> ff-ff-ff-ff-ff-ff

# Task 5 - Application Management

- **Trusted Application Store**  
	- Microsoft Store offers a complete range of applications, ensures downloading of non-malicious files. 
	- Malicious actors bind legitimate software with trojans and viruses and upload it on the internet to infect victim's computer. 
		- Therefore, downloading applications from the Microsoft Store ensures that the downloaded software is not malicious. 
	- We can access Microsoft Application Store by typing `ms-windows-store` in the Run dialogue.
- **Safe App Installation**
	- Only allow installation of applications from the Microsoft Store on your computer.
		- Can be modified slightly to fit organization needs
	- Go to `Setting > Select Apps and Features` and then select `The Microsoft Store only`.
- **Malware Removal through Windows Defender Anti Virus**
	- Complete anti-malware program capable of identifying malicious programs and taking remedial measures like quarantine. 
	- Managed through Windows Security Centre. Windows Defender primarily offers four main functionalities:
		- **Real-time protection** - Enables periodic scanning of the computer.
		- **Browser integration** - Enables safe browsing by scanning all downloaded files, etc.
		- **Application Guard** - Allows complete web session sandboxing to block malicious websites or sessions to make changes in the computer.
		- **Controlled Folder Access** - Protect memory areas and folders from unwanted applications.
- **Microsoft Office Hardening**  
	- Malicious actors abuse its functionality through macros, Flash applets, object linking etc., to achieve Remote Code Execution. 
	- Hardening varies as legitimate functionality of Microsoft Office is exploited to gain access. 
		- For example, disabling macros in a University may be helpful as no one uses it
		- However, banks cannot disable macros as they heavily rely on complex invoices and formulas through macros. 
	- Follow best practices from [Microsoft Attack Surface Reduction Rules](https://docs.microsoft.com/en-us/microsoft-365/security/defender-endpoint/attack-surface-reduction-rules-reference?view=o365-worldwide) for hardening Microsoft Office.
- **AppLocker**
	- Allows users to block specific executables, scripts, and installers from execution through a set of rules. 
	- Can easily configure them on a single PC or network through a GUI
		- Doen through Group Policy Editor, either Local or Group
		- Example, can add a rule through AppLocker to block a file based on its publisher name.
- **Browser (MS Edge)**
	- Browser available on Windows machines based on Chromium. 
	- Often acts as an entry point to a system for further pivoting and lateral movement. 
	- Utmost importance to block and mitigate critical attacks carried out through a browser that include ransomware, ads, unsigned application downloads and trojans.
- **Protecting the Browser through Microsoft Smart Screen**
	- Protects you from phishing/malware sites and software when using Microsoft Edge. 
		- Helps to make informed decisions by  
			- Displaying alerts if you are visiting any suspicious pages.
			- Vetting downloads by checking their hash, signature etc. against a malicious software database.  
			- Protecting against phishing and malicious sites by checking visited websites against a threat intelligence database.
	- To turn on the Smart Screen, go to `Settings > Windows Security > App and Browser Control > Reputation-based Protection`. Scroll down and turn on the `SmartScreen option`.
		- Open Microsoft Edge, go to Settings and then click “**Privacy, Search and Services**” - Set "**Tracking prevention**" to **Strict** to avoid tracking through ads, cookies etc.


> [!Question]
> **Windows Defender Antivirus is configured to exclude a particular extension from scanning. What is the extension?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218170219.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218170238.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218170331.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218170344.png)

> [!done] Answer
> .ps

> [!Question]
> **A Word document is received from an unknown email address. It is best practice to open it immediately on your personal computer (yay/nay)?**

> [!done] Answer
> nay

> [!Question]
> **What is the flag you received after executing the Office Hardening Batch file?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218171110.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218171048.png)

> [!done] Answer
> {THM_1101110}

# Task 6 - Storage Management

- **Data Encryption Through BitLocker**
	- Encryption ensures that you or someone you share the recovery key with can access stored content.
	- Go to `Start > Control Panel > System and Security > BitLocker Drive Encryption`. You can easily see if the option to BitLocker Drive Encryption is enabled or not.
	- A trusted Platform Module chip TPM is one of the basic requirements to support BitLocker device encryption. 
		- Keeping the BitLocker recovery key in a secure place (preferably not on the same computer) is imperative
- **Windows Sandbox**
	- To run applications safely, we can use a temporary, isolated, lightweight desktop environment called Windows Sandbox. 
		- Can install software inside this safe environment, and this software will not be a part of our host machine, it will remain sandboxed. 
	- Once closed, everything, including files, software, and states will be deleted. 
		- If you want to close the Sandbox, click the `close button,` and it will disappear. 
		- We would require Virtualization enabled on our OS to run this feature.
	- `Click Start > Search for 'Windows Features' and turn it on > Select Sandbox > Click OK to restart`
	- Opening suspicious files in a Windows Sandbox before blindly executing them in your base OS is recommended.
- **Windows Secure Boot**  
	﻿- Checks that your system is running on trusted hardware and firmware before booting 
		﻿- Ensures that your system boots up safely 
		﻿- Prevents unauthorized software access like malware
	- Already in a secure boot environment if you run with UEFI 
	- You can check the status of the secure boot by following:
		- Going to `msinfo32`
		- Check for "BIOS Mode" and "Secure Boot State"
- **Enable File Backups**  
	- Creating file backups is the best option to avoid disasters like malware attacks or hardware failure. 
	- You can enable the file backup option through  `Settings > Update and Security > Backup`
	- Therefore, the most convenient option is enabling it from the '`File History`' option 

> [!Question]
> **A security engineer has misconfigured the attached VM and stored a BitLocker recovery key in the same computer. Can you read the last six digits of the recovery key?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218221953.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218222020.png)

> [!done] Answer
> 377564

> [!Question]
> **How many characters does the BitLocker recovery key have in the attached VM??**

Refer to screenshot above

> [!done] Answer
> 48

> [!Question]
> **A backup file is placed on the Desktop of the attached VM. What is the extension of that file?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250218222235.png)

> [!done] Answer
> .bkf

![](/img/user/TryHackMe/THM_Images/dbbd403c6b1196904312c7b88f2514f2.png)

