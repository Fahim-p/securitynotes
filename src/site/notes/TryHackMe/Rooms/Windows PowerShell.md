---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/windows-power-shell/","created":"2024-12-09T18:56:00.000-05:00","updated":"2025-03-11T00:32:59.533-04:00"}
---

# Task 2 - What is PowerShell

- Cross-platform task automation solution and configuration management tool in command-line shell
- Object-oriented, based on .NET framework
- Cme.exe and batch files couldn't do much in automation and management of systems
- **Object**
	- Represents an item with properties and methods
	- Can contain file names, usernames, or sizes as data (properties) and carry functions (methods) such as copying
- **Cmdlet**
	- Returns objects that retain their properties and methods
- More powerful and flexible data manipulation since they don’t need additional parsing of text

> [!Question] 
**What do we call the advanced approach used to develop PowerShell?**

> [!Done] Answer
Object-Oriented

# Task 3 - PowerShell Basics

**cmdlets**
- Follows a consistent "Verb-Noun" naming convention
	- Examples
		- `Get-Content`, Gets content of file and displays it
		- `Set-Location`, Changes working directory

| Verb | Verb Describes the action                         |
| ---- | ------------------------------------------------- |
| Noun | Specifies the object on which action is performed |

**Get-Command**, Lists all available and executable cmdlets, functions, aliases, and scripts

![image1 6.png](/img/user/TryHackMe/THM_Images/bc804348591238889c181ce0c39ff18c.png)
        
Can filter by property values like function. For example, `Get-Command -CommandType "Function"`

![image2 6.png](/img/user/TryHackMe/THM_Images/89431d32836e8c02574055ae4ed0f3db.png)

**Get-Help**, Provides detailed information about cmdlets, including usage, parameters, and examples, Can add parameters like `-example

![image3 6.png](/img/user/TryHackMe/THM_Images/6d27a8f9d1f6ed1f409519a889b79fb8.png)

**Get-Alias**, Shortcuts or alternative names for cmdlets 
        
![image4 5.png](/img/user/TryHackMe/THM_Images/ff5b59c567119285a74ef5bcd4d12e4f.png)
        
- **Find-Module**
	- Search for collections of cmdlets through online repositories
	- Can use wildcard to find modules with similar name
        
![image5 6.png](/img/user/TryHackMe/THM_Images/5d1819c1e1efa7087e60aa97a765216c.png)
        
- **Install-Module**, Downloads and installs modules from repositories

![image6 6.png](/img/user/TryHackMe/THM_Images/ba99ea539e44444cf906b5951dd8477e.png)
        
> [!Question] 
**How would you retrieve a list of commands that start with the verb Remove?**

![image7 6.png](/img/user/TryHackMe/THM_Images/c8affb0b46247a190774af6d8f56aff1.png)

> [!Done] Answer: 
`Get-Command -Name Remove*`

> [!Question] 
**What cmdlet has its traditional counterpart echo as an alias?**

![image8 4.png](/img/user/TryHackMe/THM_Images/c98d36efe465e5e62322ada501427939.png)

> [!Done] Answer
Write-Output

> [!Question] 
**What is the command to retrieve some example usage for the cmdlet New-LocalUser?**

![image9 4.png](/img/user/TryHackMe/THM_Images/4d2b4f43eb04c570bbeac5180d9cc951.png)

> [!Done] Answer
Get-Help New-LocalUser -Examples

# Task 4 - Navigating the File System and Working with Files

- **Get-ChildItem**
	- Similar to dir or ls, lists files and directories specified in -Path parameter
	- If no path, then prints in current directory

![image10 3.png](/img/user/TryHackMe/THM_Images/e64e23a26f94a76717a6826e1be667b0.png)
        
- **Set-Location**, Changes directories, similar to cd

![image11 3.png](/img/user/TryHackMe/THM_Images/fe7c8a52c6514187eae12557b5a6b549.png)
        
- **New-Item**, Creates an item in PowerShell, need to specify path of item and it's type (file or directory)

![image12 3.png](/img/user/TryHackMe/THM_Images/24f0ae8b2290997d38459547d536c8f0.png)
        
- **Remove-Item**, Removes both directories and files

![image13 2.png](/img/user/TryHackMe/THM_Images/0f042d08a881582117d4cc056eca6098.png)
        
- **Copy-Item**, Copies files and directories

![image14 2.png](/img/user/TryHackMe/THM_Images/1ebd9c28578b0cd68f91f7b6659065fe.png)
        
- **Move-Item**, Moves a file or a directory
- **Get-Content**, Read and displays content of file

![image15 2.png](/img/user/TryHackMe/THM_Images/b982978af6b97245905ca90cefe2ed91.png)
        
> [!question] 
**What cmdlet can you use instead of the traditional Windows command 'type'?**

> [!done] Answer
`Get-Content`

> [!question] 
**What PowerShell command would you use to display the content of the "C:\Users" directory?**

![image16 2.png](/img/user/TryHackMe/THM_Images/a906b6da641ef295a6671c2de4dd31c3.png)

> [!done] Answer
`Get-ChildItem -Path C:\Users\`

> [!Question] 
**How many items are displayed by the command described in the previous question?**

> [!done] Answer
4

# Task 5 - Piping, Filtering, and Sorting Data

- Piping allows output of one command to be used as the input of another
- Can pass objects rather than just text
	- Carries data, but properties and methods that describe/interact with data

Example, list files and then sort by size
    
![image17 2.png](/img/user/TryHackMe/THM_Images/827ae72c2dc296c216db7256e105972d.png)
    
**Where-Object**, Can filter objects based on specified conditions
        
![image18 2.png](/img/user/TryHackMe/THM_Images/c4796d80d326ad20d700ccac3ccfa348.png)
        
**Comparison operators**

|-eq: "equal to"|Only objects from results based on specified criteria.|
|---|---|
|-ne: "not equal".|Exclude objects from results based on specified criteria.|
|-gt: "greater than".|Only objects which exceed a specified value.|
|-ge: "greater than or equal to".|A combination of -gt and -eq.|
|-lt: "less than".|Only objects which are strictly below a certain value.|
|-le: "less than or equal to".|A combination of -lt and -eq|
    
- **-like**, Properties that match a specified pattern

![image19 2.png](/img/user/TryHackMe/THM_Images/9be50f79df5420d1f7d6b13a7a7323a6.png)

- **Select-Object**, Select specific properties from objects or limit number of objects returned

![image20 2.png](/img/user/TryHackMe/THM_Images/f7b49b6776fefd671a98f754ba523c64.png)

- **Select-String**, Searches for text patterns within files, similar to grep

![image21 2.png](/img/user/TryHackMe/THM_Images/d016a2a7a3610edc496ad7bfc80d6e79.png)

> [!Question] 
**How would you retrieve the items in the current directory with size greater than 100?**

> [!done] Answer
`Get-ChildItem | Where-Object -Property Length -gt 100`

# Task 6 - System and Network Information

**Get-ComputerInfo**, Retrieves system information, snapshot of entire system configuration

![image22 1.png](/img/user/TryHackMe/THM_Images/a9fd8e38b759d99d226fbe9852b757df.png)
        
**Get-LocalUser**, Lists all local user accounts on system

![image23 1.png](/img/user/TryHackMe/THM_Images/5413cd3a0829989668b0081f0393492b.png)
        
**Get-NetIpConfiguration**, Gives network information, like IP addresses, DNS servers, etc.
        
![image24 1.png](/img/user/TryHackMe/THM_Images/2192d56506f95ed864fa08abb9cdf020.png)
        
**Get-NetIpAddress**, Show details for all IP addresses configured on system, including inactive ones

![image25 1.png](/img/user/TryHackMe/THM_Images/0a0ec2d496a7993869bf60d2387e069e.png)

> [!Question] 
**Other than your current user and the default "Administrator" account, what other user is enabled on the target machine?**

![image26.png](/img/user/TryHackMe/THM_Images/8c78effedd5991063fdfd651b1e67fa5.png)

> [!Done] Answer
p1r4t3

> [!Question] 
**This lad has hidden his account among the others with no regard for our beloved captain! What is the motto he has so bluntly put as his account's description?**

> [!Done] Answer
A merry life and a short one.

> [!Question] 
**Now a small challenge to put it all together. This shady lad that we just found hidden among the local users has his own home folder in the "C:\Users" directory. Can you navigate the filesystem and find the hidden treasure inside this pirate's home?**

![1000](/img/user/TryHackMe/THM_Images/32d90c2435c817fd302aeb2e02d6d291.png)

> [!done] Answer
THM{p34rlInAsh3ll}

# Task 7 - Real-Time System Analysis

**Get-Process**, Provides detailed view off all currently running processes
        
![image28.png](/img/user/TryHackMe/THM_Images/1e6d52b7547b74eefec76d4dbb101aa6.png)
        
**Get-Service**, Gives status on services on machine
        
![image29.png](/img/user/TryHackMe/THM_Images/e5c9ef2420336c837af8831aa010f307.png)
        
**Get-NetTCPConnection**, Displays current TCP connections, on both local and remote endpoints
        
![image30.png](/img/user/TryHackMe/THM_Images/746987f89882504a1957f7c5f51e8ef0.png)
        
**Get-FileHash**, Generates file hashes
        
![image31.png](/img/user/TryHackMe/THM_Images/b3c013d8af072481899f9ef4eb579cf4.png)

> [!question] 
**In the previous task, you found a marvellous treasure carefully hidden in the target machine. What is the hash of the file that contains it?**

![image32.png](/img/user/TryHackMe/THM_Images/d5765df454e0a4d75c62fde3574a4b88.png)

> [!done] Answer
71FC5EC11C2497A32F8F08E61399687D90ABE6E204D2964DF589543A613F3E08

> [!question] 
**What property retrieved by default by Get-NetTCPConnection contains information about the process that has started the connection?**

> [!done] Answer
OwningProcess

> [!question] 
**It's time for another small challenge. Some vital service has been installed on this pirate ship to guarantee that the captain can always navigate safely. But something isn't working as expected, and the captain wonders why. Investigating, they find out the truth, at last: the service has been tampered with! The shady lad from before has modified the service DisplayName to reflect his very own motto, the same that he put in his user description. With this information and the PowerShell knowledge you have built so far, can you find the service name?**

![image33.png](/img/user/TryHackMe/THM_Images/f088f1df10dd83a9fc2dea5e40f7d27a.png)

> [!done] Answer
p1r4t3-s-compass

# Task 8 - Scripting

- **Invoke-Command**
    - Needed to execute commands on remote systems
    - Enables automation of tasks across multiple machines
        
![image34.png](/img/user/TryHackMe/THM_Images/1f62a809e129ce183d30d20cf615fc8c.png)
        
- **-ScriptBlock {…}**
	- Allows for any command execution on remote computer
	- Same result as if it were typed in local session

> [!question] 
**What is the syntax to execute the command Get-Service on a remote computer named "RoyalFortune"? Assume you don't need to provide credentials to establish the connection?**

> [!done] Answer
`Invoke-Command -ComputerName RoyalFortune -ScriptBlock { Get-Service }`