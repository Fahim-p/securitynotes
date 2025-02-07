---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/capa-the-basics/","created":"2024-11-25T17:41:00.000-05:00","updated":"2025-02-06T21:51:30.209-05:00"}
---

# Task 1 - Introduction

- Static analysis tool
	- Common Analysis Platform for Artifacts
- Identify capabilities present in executables, binaries, .NET modules, shellcode
- Analyzes files, applies rules that describe common behaviors
	- Tells what the program is able to do
- Automated tool for reverse engineering
# Task 2 - Tool Overview: How CAPA Works

Example code to run tool in PowerShell

```
capa.exe .\filename
```

| Option            | Description                      | Sample Syntax               |
| ----------------- | -------------------------------- | --------------------------- |
| -h or --help      | Show this help message and exit. | capa -h                     |
| -v or --verbose   | Verbose result document          | capa.exe .\cryptbot.bin -v  |
| -vv or --vverbose | Very verbose result document.    | capa.exe .\cryptbot.bin -vv |

![](/img/user/TryHackMe/THM_Images/6869943b68bf1e1021f011dbbcf13c96.png)
![image 16.png](/img/user/TryHackMe/THM_Images/6869943b68bf1e1021f011dbbcf13c96.png)

> [!Question]
> **What command-line option would you use if you need to check what other parameters you can use with the tool? Use the shortest format.**

> [!Success] Answer
>  -h

> [!Question]
>  **What command-line options are used to find detailed information on the malware's capabilities? Use the shortest format.**

> [!Success] Answer 
> -v

> [!Question]
> **What command-line options do you use to find very verbose information about the malware's capabilities? Use the shortest format.**

> [!Success] Answer
> -vv

> [!Question]
> **What PowerShell command will you use to read the content of a file?**

> [!Success] Answer 
> Get-Content
# Task 3 - Dissecting CAPA Results Part 1: General Information, MITRE and MAEC

First part contains basic info about the file

![image 17.png](/img/user/TryHackMe/THM_Images/765bff973ca53703e495e3e0f946dc72.png)

Uses MITRE Attack Framework as apart of the output. Helps analysts or defenders map the file's behavior to the adversary's playbook

![image 18.png](/img/user/TryHackMe/THM_Images/0cfe4df2df7908b07b9f4ae5ef3db8e7.png)
    
**MITRE table**

| Format                                                                                                 | Sample                                                                                    | Explanation                                                                                                                                                                                                            |
| ------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ATT&CK Tactic::ATT&CK Technique::Technique Identifier                                                  | Defense Evasion::Obfuscated Files or Information::T1027                                   | DEFENSE EVASION = ATT&CK Tactic  <br>Obfuscated Files or Information = ATT&CK Technique  <br>T1027 = Technique Identifier                                                                                              |
| ATT&CK Tactic::ATT&CK Technique::ATT&CK Sub-Technique::Technique Identifier[.]Sub-technique Identifier | Defense Evasion::Obfuscated Files or Information::Indicator Removal from Tools::T1027.005 | DEFENSE EVASION = ATT&CK Tactic  <br>Obfuscated Files or Information = ATT&CK Technique  <br>Indicator Removal from Tools = ATT&CK Sub-Technique  <br>T1027 = Technique Identifier  <br>005 = Sub-Technique Identifier |
    
**MAEC**
- Malware Attribute Enumeration and Characterization
- Language to encode and explain details about malware
- Standardized system of tracking/analyzing complexities of malware
    
![image 19.png](/img/user/TryHackMe/THM_Images/1af1d1471d485e3c2dff6132d4d180bc.png)

**MAEC Table**

| MAEC Value | Description                                                                   |
| ---------- | ----------------------------------------------------------------------------- |
| Launcher   | Exhibits behaviors that trigger specific actions similar to malware behavior. |
| Downloader | Exhibits behaviors where it downloads and executes other files, more complex  |

- When tagged with “**launcher**”, indicates that the file demonstrates behavior similar to:
	- Dropping additional payloads
        - Activating persistence mechanisms
        - Connecting to command-and-control (C2) servers
        - Executing specific functions
- When tagged with “**Downloader**”, indicates that the file demonstrates behavior similar to:
	- Fetching additional payloads or resources from the internet
        - Pulling in updates
        - Executing secondary stages
        - Retrieving configuration files

> [!Question]
> **What is the sha256 of cryptbot.bin?**

![image 20.png](/img/user/TryHackMe/THM_Images/8aa0a5f3514deb2612678d968040d606.png)

> [!Success] Answer
> ae7bc6b6f6ecb206a7b957e4bb86e0d11845c5b2d9f7a00a482bef63b567ce4c

> [!Question]
> **What is the Technique Identifier of Obfuscated Files or Information?**

![image 21.png](/img/user/TryHackMe/THM_Images/e32f95c8e342f976be2effcb740d54ab.png)

> [!Success] Answer
> T1027

> [!Question]
> **What is the Sub-Technique Identifier of Obfuscated Files or Information::Indicator Removal from Tools?**

Based off screenshot above

> [!Success] Answer
> T1027.005

> [!Question]
> **When CAPA tags a file with this MAEC value, it indicates that it demonstrates behavior similar to, but not limited to, Activating persistence mechanisms?**

> [!Success] Answer
> Launcher

> [!Question]
> **When CAPA tags a file with this MAEC value, it indicates that the file demonstrates behavior similar to, but not limited to, Fetching additional payloads or resources from the internet?**

> [!Success] Answer
> Downloader
# Task 4 - Dissecting CAPA Results Part 2: Malware Behavior Catalogue

![image 22.png](/img/user/TryHackMe/THM_Images/db8689ef4404fc2f06e71e8cdc7c6ece.png)

**Malware Behavior Catalogue (MBC)**
- Supports various aspects of malware analysis
- Labelling, similarity analysis, standardized reporting
- Can reference to ATT&CK methods with different name
- Can be represented in two formats:

| Format                                  | Sample                                                                              | Explanation                                                                                                                                 |
| --------------------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| OBJECTIVE::Behavior::Method[Identifier] | ANTI-STATIC ANALYSIS::Executable Code Obfuscation::Argument Obfuscation [B0032.020] | Anti-static Analysis = OBJECTIVE  <br>Executable Code Obfuscation = BEHAVIOR  <br>Argument Obfuscation = METHOD  <br>BOO32.020 = IDENTIFIER |
| OBJECTIVE::Behavior::[Identifier]       | COMMUNICATION::HTTP Communication:: [C0002]                                         | COMMUNICATION = OBJECTIVE  <br>HTTP Communication = BEHAVIOR  <br>C0002 = IDENTIFIER                                                        |

**Objective**    

Based on ATT&CK tactics in the context of malware behavior

| Objective                | Explanation                                                                                                                                            |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Anti-Behavioral Analysis | Avoid detection by hindering behavioral analysis using tools like sandboxes or debuggers.                                                              |
| Anti-Static Analysis     | Obstruct or add complexity to static analysis,                                                                                                         |
| Collection               | Identifying and gathering information from the targeted machine or network.                                                                            |
| Command and Control      | Establishes communication with compromised systems through various methods such as command and control servers, peer-to-peer networks, or other means. |
| Credential Access        | Steal account credentials, such as usernames and passwords.                                                                                            |
| Defense Evasion          | Bypass and circumvent the various detection and security mechanisms present.                                                                           |
| Discovery                | Collect detailed information about the configuration and setup of the system or network environment.                                                   |
| Execution                | Execute unauthorized commands or code on a targeted computer system without the user’s consent.                                                        |
| Exfiltration             | Infiltrate computer systems or networks to steal and extract sensitive data.                                                                           |
| Impact                   | Manipulate, disrupt, or damage computer systems and data. It can enter computers through infected emails, compromised websites, etc.                   |
| Lateral Movement         | Spread through the network, either actively through machine access or passively                                                                        |
| Persistence              | Developed with the capability to remain undetected and operational on a computer system for an extended period.                                        |
| Privilege Escalation     | Infiltrate a computer system or network to gain elevated permissions or control.                                                                       |

**Micro-Objective**
    
Actions exhibited by potentially malicious software that isn't fully malicious or serve multiple objectives, typically abused
    
| Micro-Objective | Description                                                                        |
| --------------- | ---------------------------------------------------------------------------------- |
| PROCESS         | Creating Process, Setting Thread Context, Terminating Process, and Checking Mutex. |
| MEMORY          | Allocating Memory, Changing Memory Protection, and Freeing Memory.                 |
| COMMUNICATION   | DNS, FTP, HTTP, ICMP, SMTP, etc. network traffic.                                  |
| DATA            | Checking strings, compressing, decoding and encoding data                          |

**MBC Behaviors**
    
| Objective                             | Behavior                          | Identifiers | Explanation                                                                                                                                               |
| ------------------------------------- | --------------------------------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ANTI-BEHAVIORAL ANALYSIS              | Virtual Machine Detection         | B0009       | Checks to see if it is running in a virtual environment.                                                                                                  |
| ANTI-STATIC ANALYSIS                  | Executable Code Obfuscation       | B0032       | Intentionally obscured to prevent static code analysis.                                                                                                   |
| EXECUTION                             | Command and Scripting Interpreter | E1059       | Exploits command and script interpreters to run malicious commands, scripts, or binaries.                                                                 |
| DISCOVERY                             | File and Directory Discovery      | E1083       | Searches for specific files in particular locations by enumerating files and directories.                                                                 |
| ANTI-STATIC ANALYSIS, DEFENSE EVASION | Obfuscated Files or Information   | E1027       | Obfuscates files or information by encoding, encrypting, or otherwise, making them hard to analyze. It can also encode or encrypt malware samples itself. |

**Micro Behaviors**
- Actions exhibited by malware that aren't necessarily malicious and may serve various objectives
- Just because a behavior is categorized as low-level does not mean it is harmless

|Micro-Objective|Micro-Behaviors|Identifiers|Explanation|
|---|---|---|---|
|MEMORY|Allocate Memory|C0007|Uses memory allocation as part of its strategy to unpack itself and execute its malicious activities.|
|PROCESS|Create Process|C0017|Process via WMI or shellcode. Also create a suspended process.|
|COMMUNICATION|HTTP Communication|C0002|Initiate HTTP communications.|
|DATA|Check String|C0019|Inspect strings specific characteristics|
|ANTI-STATIC ANALYSIS, DEFENSE EVASION|Obfuscated Files or Information|E1027|Obfuscates files or information by encoding, encrypting. Can also encode or encrypt malware samples itself.|
|DATA|Encode Data|C0026|Encode data using base64 and XOR.|
|FILE SYSTEM|Create Directory|C0046|Can create a directory.|
|FILE SYSTEM|Delete File|C0047|Can Delete a file.|
|FILE SYSTEM|Read File|C0051|Can read a file.|
|FILE SYSTEM|Writes File|C0052|Can write to a file.|    

**Methods**
    
| Behavior                        | Methods or sub-technique    | Identifier | Explanation                                                                                     |
| ------------------------------- | --------------------------- | ---------- | ----------------------------------------------------------------------------------------------- |
| Executable Code Obfuscation     | Argument Obfuscation        | B0032.020  | Simple number or string arguments to API calls are calculated at runtime                        |
| Executable Code Obfuscation     | Stack Strings               | B0032.017  | Build and decrypt strings on the stack at each use, then discard to avoid obvious references.   |
| HTTP Communication              | Read Header                 | C0002.014  | HTTP read header.                                                                               |
| Encode Data                     | Base64                      | C0026.001  | Encode data using Base64.                                                                       |
| Encode Data                     | XOR                         | C0026.002  | Use XOR to encode data.                                                                         |
| Obfuscated Files or Information | Encoding-Standard Algorithm | E1027.m02  | Encoding malware samples, files, or other information uses a standard algorithm (e.g., base64). |

Example recap of the table

![image 23.png](/img/user/TryHackMe/THM_Images/c6e61be57a3527447c7dad2748350ac2.png)

| Label         | Value       | Explanation                                                                                                   |
| ------------- | ----------- | ------------------------------------------------------------------------------------------------------------- |
| MBC Objective | DATA        | exhibiting behaviors such as, but not limited to, checking strings, compressing, decoding, and encoding data. |
| MBC Behavior  | Encode Data | Malware has the capability to encode data using base64 and XOR.                                               |
| Method        | Base64      | Malware may encode data using Base64.                                                                         |
| Identifier    | C0026.001   | identifier relays information about a behavior.                                                               |
    
> [!Question]
> **What serves as a catalogue of malware objectives and behaviors?**

> [!Success] Answer
> Malware Behavior Catalogue

> [!Question]
>  **Which field is based on ATT&CK tactics in the context of malware behavior?**

> [!Success] Answer
> Objective

> [!Question]
> **What is the Identifier of "Create Process" micro-behavior?**

> [!Success] Answer
> C0017

> [!Question]
> **What is the behavior with an Identifier of B0009?**

> [!Success] Answer
> Virtual Machine Detection

> [!Question]
> **Malware can be used to obfuscate data using base64 and XOR. What is the related micro-behavior for this?**

> [!Success] Answer
> Encode Data

> [!Question]
> **Which micro-behavior refers to "Malware is capable of initiating HTTP communications"?**

> [!Success] Answer
> HTTP Communication

# Task 5 - Dissecting CAPA Results Part 3: Namespaces

![image 24.png](/img/user/TryHackMe/THM_Images/3c8cc8c4be2bc74c618d6b6a6ddb0568.png)

|Format|Sample|Explanation|Explanation|
|---|---|---|---|
|Capability(Rule Name)::TLN(Top-Level Namespace)/Namespace|reference anti-VM strings::Anti-Analysis/anti-vm/vm-detection|Reference anti-VM strings = Capability(Rule Name) Anti-Analysis = TLN or Top-Level Namespace anti-vm/vm-detection = Namespace|Simple number or string arguments to API calls are calculated at runtime, making analysis more difficult.|

| Top-Level Namespace (TLN) | Explanation                                                                                                                                                                                                                                                                     |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| anti-analysis             | Rules specifically designed to detect behaviours exhibited by malware to evade analysis.                                                                                                                                                                                        |
| Collection                | Rules that malware may enumerate and collect for exfiltration or other purposes.                                                                                                                                                                                                |
| Communication             | Rules that pertain to different communication behaviours demonstrated by malware. This encompasses how malware interacts with networks                                                                                                                                          |
| Compiler                  | Rules and configurations for recognizing specific build environments or compilers employed in generating executables.                                                                                                                                                           |
| data-manipulation         | Rules that govern the behaviours involved in altering data within executable files                                                                                                                                                                                              |
| executable                | Rules pertaining to the attributes in executable files.                                                                                                                                                                                                                         |
| host-interaction          | Rules related to behaviors involving interactions with the host system. This encompasses how malware interacts with its environment.                                                                                                                                            |
| impact                    | Rules related to the potential consequences or effects of a program’s behavior. It may include behaviors related to establishing remote access, data exfiltration, destruction, or modification.”                                                                               |
| internal                  | Rules meant for internal purposes within the CAPA tool, serving as the behind-the-scenes aspect of rule development and execution.                                                                                                                                              |
| lib                       | Building blocks to create other rules                                                                                                                                                                                                                                           |
| linking                   | Rules to identify behaviors involving linking or dynamically loading external code or libraries during program execution. Detecting external dependencies helps analysts understand the malware’s capabilities. External libraries also introduce an additional attack surface. |
| load-code                 | Rules and regulations related to the behaviors associated with dynamically loading or executing code during program execution.                                                                                                                                                  |
| malware-family            | Rules related to behaviors that are linked to particular malware families or groups. Serves as a way to identify the distinct characteristics or “signatures” associated with known malware families.                                                                           |
| nursery                   | Staging ground that contains rules for those who are not quite polished                                                                                                                                                                                                         |
| persistence               | Rules related to behaviors associated with maintaining access or persistence within a compromised system.                                                                                                                                                                       |
| runtime                   | Rules that seek to identify the language or platform on which the program runs.                                                                                                                                                                                                 |
| targeting                 | Rules related to behaviors exhibited by programs that interact with ATMs.                                                                                                                                                                                                       |

Below is representation of the namespace to the rules that CAPA uses.

![5e6bbe59a46ee9407fd65bbe-1728863959663.png](/img/user/TryHackMe/THM_Images/4de6efb9e488a8f2bdec3244fffbb142.png)

> [!Question]
> **Which top-level Namespace contains a set of rules specifically designed to detect behaviours, including obfuscation, packing, and anti-debugging techniques exhibited by malware to evade analysis?**

> [!Success] Answer
> Anti-analysis

> [!Question]
> **Which namespace contains rules to detect virtual machine (VM) environments? Note that this is not the TLN or Top-Level Namespace?**

> [!Success] Answer
> anti-vm/vm-detection

> [!Question]
> **Which Top-Level Namespace contains rules related to behaviours associated with maintaining access or persistence within a compromised system? This namespace is focused on understanding how malware can establish and maintain a presence within a compromised environment, allowing it to persist and carry out malicious activities over an extended period?**

> [!Success] Answer
> Persistence

> [!Question]
> **Which namespace addresses techniques such as String Encryption, Code Obfuscation, Packing, and Anti-Debugging Tricks, which conceal or obscure the true purpose of the code?**

> [!Success] Answer
> Obfuscation

> [!Question]
> **Which Top-Level Namespace Is a staging ground for rules that are not quite polished?**

> [!Success] Answer
> Nursery

# Task 6 - Dissecting CAPA Results Part 4: Capability

![image 25.png](/img/user/TryHackMe/THM_Images/1b3a64736bbe3c9d20b9cfea4f97af92.png)

Capabilities is mainly the name of the rule, (YML file), located under namespaces

![image 26.png](/img/user/TryHackMe/THM_Images/e89dd7c2664b45c0874f5b5bb86be66f.png)

Explanation of the table above

|Label|Value|Explanation|
|---|---|---|
|Capability|reference base64 string|Encode data using a base64 scheme.|
|Top-Level Namespace|data-manipulation|Rules that govern the behaviors involved in altering data within executable files.|
|Namespace|encoding/base64|Rules for encoding and decoding data using Base64 and XOR|
|Rule YAML File Matched?|reference-base64-string.yml|Remember that the capability's name is also the rule's name with an additional dash (-) character between spaces.|

> [!Question]
> **What rule yaml file was matched if the Capability or rule name is check HTTP status code?**

> [!done] Answer
> check-HTTP-status-code.yml

> [!Question]
> **What is the name of the Capability if the rule YAML file is reference-anti-vm-strings.yml?**

> [!done] Answer
> reference anti-VM strings

> [!Question]
> **Which TLN or Top-Level Namespace includes the Capability or rule name run PowerShell expression?**

> [!done] Answer
> Load-code

> [!Question]
> 
> **Check the conditions inside the check-for-windows-sandbox-via-registry.yml rule file from this link. What is the value of the API that ends in Ex is it looking for?**
>     
>     https://github.com/MBCProject/capa-rules-1/blob/master/anti-analysis/anti-vm/vm-detection/check-for-windows-sandbox-via-registry.yml
>     

> [!done] Answer
> RegOpenKeyEx