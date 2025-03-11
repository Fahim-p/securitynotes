---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/flare-vm-arsenal-of-tools/","created":"2024-12-02T18:33:00.000-05:00","updated":"2025-03-11T00:32:59.146-04:00"}
---

# Task 2 - Arsenal of Tools

- **Reverse Engineering & Debugging**
	- **Ghidra** - Reverse engineering suite.
	- **x64dbg** - Debugger for binaries in x64 and x32 formats.
	- **OllyDbg** - Debugger for reverse engineering at the assembly level.
	- **Radare2** - Platform for reverse engineering.
	- **Binary Ninja** - Sisassembling and decompiling binaries.
	- **PEiD** - Packer, cryptor, and compiler detection tool.
- **Disassemblers & Decompilers**
	- **CFF Explorer** - A Portable Executable (PE) editor designed to analyze and edit PE files.
	- **Hopper Disassembler** - A Debugger, disassembler, and decompiler.
	- **RetDec** - Decompiler for machine code.
- **Static and Dynamic Analysis**
	- **Process Hacker** - Memory editor and process watcher.
	- **PEview** - A PE file viewer for analysis.
	- **Dependency Walker** - Displays an executable’s DLL dependencies.
	- **DIE (Detect It Easy)** - A packer, compiler, and cryptor detection tool.
- **Forensic and Incident Response**
	- **Volatility** - RAM dump analysis framework.
	- **Rekall** - Framework for memory forensics.
	- **FTK Imager** - Disc image acquisition and analysis tool.
- **Network Analysis**
	- **Wireshark** - Network protocol analyzer for traffic recording and examination.
	- **Nmap** - Vulnerability detection and network mapping tool.
	- **Netcat** - Read and write data across network connections.
- **File Analysis**
	- **FileInsight** - Looking and editing binary files.
	- **Hex Fiend** - Hex editor.
	- **HxD** - Binary file viewing and hex editor.
- **Scripting & Automation**
	- **Python** - Mainly automation-focused on Python modules and tools.
	- **PowerShell Empire** - Framework for PowerShell post-exploitation
- **Sysinternals Suite**
	- **Autoruns** - Shows what executables are configured to run during system boot-up.
	- **Process Explorer** - Provides information about running processes.
	- **Process Monitor** -Monitors and logs real-time process/thread activity.

> [!Question] 
**Which tool is an Open-source debugger for binaries in x64 and x32 formats?**

> [!Success] Answer
**x64dbg**

> [!Question] 
**What tool is designed to analyze and edit Portable Executable (PE) files?**

> [!Success] Answer 
CFF Explorer

> [!Question] 
**Which tool is considered a sophisticated memory editor and process watcher?**

> [!Success] Answer
Process Hacker

> [!Question] 
**Which tool is used for Disc image acquisition and analysis for forensic use?**

> [!Success] Answer
FTK Imager

> [!Question] 
What tool can be used to view and edit a binary file?

> [!Success] Answer
HxD

# Task 3 - Commonly Used Tools for Investigation: Overview

|Tool|Investigative Value|
|---|---|
|Procmon|Tracks system activity. See, record, and keep track of system and Windows file activity in real-time.|
|Process Explorer|See Process of the Parent-child relationship, DLLs loaded, and its path.|
|HxD|Files can be examined or altered via hex editing.|
|Wireshark|Observing and investigating network traffic.|
|CFF Explorer|Generate file hashes for integrity verification, authenticate the source of system files, and validate their validity.|
|PEStudio|Static analysis or studying executable file properties without running the files.|
|FLOSS|Extracts and de-obfuscates all strings from malware programs using advanced static analysis techniques.|

> [!Question] 
**Which tool was formerly known as FLARE Obfuscated String Solver?**

> [!Success] Answer
FLOSS

> [!Question] 
**Which tool offers in-depth insights into the active processes running on your computer?**

> [!Success] Answer
Process Explorer

> [!Question] 
**By using the Process Explorer (procexp) tool, under what process can we find smss.exe?**

![image 53.png](/img/user/TryHackMe/THM_Images/215275cdf2ad23a824708f7e0ef733c7.png)

> [!Success] Answer
System

> [!Question] 
**Which powerful Windows tool is designed to help you record issues with your system's apps?**

> [!Success] Answer
Procmon

> [!Question] 
**Which tool can be used for Static analysis or studying executable file properties without running the files?**

> [!Success] Answer
PEStudio

> [!Question] 
**Using the tool PEStudio to open the file `cryptominer.bin` in the Desktop\Sample folder, what is the sha256 value of the file?**

![image 54.png](/img/user/TryHackMe/THM_Images/8f5f8015f9f71abcde39155b4eb12628.png)

> [!Success] Answer
E9627EBAAC562067759681DCEBA8DDE8D83B1D813AF8181948C549E342F67C0E

> [!Question] 
**Using the tool PEStudio to open the file `cryptominer.bin` in the Desktop\Sample folder, how many functions does it have?**

![image 55.png](/img/user/TryHackMe/THM_Images/a8aa4b2290dc7081626bc5673557d524.png)

> [!Success] Answer
102

> [!Question] 
**What tool can generate file hashes for integrity verification, authenticate the source of system files, and validate their validity?**

> [!Success] Answer
CFF Explorer

> [!Question] 
**Using the tool CFF Explorer to open the file `possible_medusa.txt` in the Desktop\Sample folder, what is the MD5 of the file?**

![image 56.png](/img/user/TryHackMe/THM_Images/89023208e6a86055f9eedd5842542df8.png)

> [!Success] Answer
646698572AFBBF24F50EC5681FEB2DB7

> [!Question] 
**Use the CFF Explorer tool to open the file `possible_medusa.txt` in the Desktop\Sample folder. Then, go to the DOS Header Section. What is the e_magic value of the file?**

![image 57.png](/img/user/TryHackMe/THM_Images/5ddf6f9ed3a41926693d4eb6b862e333.png)

> [!Success] Answer
5A4D

# Task 4 - Analyzing Malicious Files!

- Example, Given suspicious “windows.exe” file, want to examine for analysis
    ![image 58.png](/img/user/TryHackMe/THM_Images/cf43c3b6f1a96a4dae5128a852b027c0.png)
    
## PEStudio

Can open file and check for hashes using websites like [VirusTotal](https://www.virustotal.com/gui/) to see if it’s recommended
    
![image 59.png](/img/user/TryHackMe/THM_Images/a7cc8262f86d71c562d41715bfedb9d6.png)
![image 60.png](/img/user/TryHackMe/THM_Images/4d7d9946026c7e6439cf5d2a70c67a91.png)
        
Can also check for description to see what it refers to, which can be misleading to evade discovery. Description says “REGEDIT”, even though REGEDIT tools are usually found in System32 directory rather than user’s download location

![image 61.png](/img/user/TryHackMe/THM_Images/dabf6c28e91062e398621f325e62b490.png)

Can check for the versions and see company name and comments
        
![image 62.png](/img/user/TryHackMe/THM_Images/f803e0cebb44bfaf0f7c962f36a3dfda.png)

No rich-header is usually tactic of obfuscation by malware

![image 63.png](/img/user/TryHackMe/THM_Images/5e61e05528b0887c7485d376c0a0673f.png)

Can also check for functions to see what API calls the file has imported

![image 64.png](/img/user/TryHackMe/THM_Images/f584160df022a03488f48af002e627fb.png)
## FLOSS

Can run the tool with PowerShell and output it into a .txt file to analyze the results.

```
FLOSS.exe .\windows.exe > windows.txt
```

![image 65.png](/img/user/TryHackMe/THM_Images/b32aea66954513359e1497766be757bf.png)

![image 66.png](/img/user/TryHackMe/THM_Images/952dd0795762d71365b7588c4076eeb7.png)
        
## Process Explorer and Process Monitor

For this example, we ran the “cobaltstrike.exe” and opened up Process Explorer to see the destination it connects to and the state it sends

![image 67.png](/img/user/TryHackMe/THM_Images/2125a19d70f205e88813ad0e914b360d.png)

When it comes to ProcMon, we have to set up the filter in order to find the process more efficiently

![image 68.png](/img/user/TryHackMe/THM_Images/c8c53aee22c687252cbacd896b3648b8.png)        

> [!Question] 
**Using PEStudio, open the file windows.exe. What is the entropy value of the file windows.exe?**

![image 69.png](/img/user/TryHackMe/THM_Images/23c81c0c85e1ceebd4d60d6eeef41325.png)

> [!Success] Answer 
7.999

> [!Question] 
**Using PEStudio, open the file windows.exe, then go to manifest (administrator section). What is the value under requestedExecutionLevel?**

![image 70.png](/img/user/TryHackMe/THM_Images/ab91eeb0df6b2ba69740bd98b9cc7dcf.png)

> [!Success] Answer
requireAdministrator

> [!Question] 
**Which function allows the process to use the operating system's shell to execute other processes?**

![image 71.png](/img/user/TryHackMe/THM_Images/fe5288ce69d00712d9b9fc9b2466f0b7.png)

> [!Success] Answer
set_UseShellExecute

> [!Question] 
**Which API starts with R and indicates that the executable uses cryptographic functions?**

![image 72.png](/img/user/TryHackMe/THM_Images/1d48a43a1cbb7bdcfb371e8a94d6fa0d.png)

> [!Success] Answer
RijndaelManaged

> [!Question] 
**What is the Imphash of cobaltstrike.exe?**

![image 73.png](/img/user/TryHackMe/THM_Images/7ec1fe5ae8e718606f93d54e5687d339.png)

> [!Success] Answer
92EEF189FB188C541CBD83AC8BA4ACF5

> [!Question] 
**What is the defanged IP address to which the process cobaltstrike.exe is connecting?**

![image 74.png](/img/user/TryHackMe/THM_Images/1505a7fc6e8b17cb2201f8251c894f4d.png)

> [!Success] Answer: 
47.120.46.210

> [!Question] 
**What is the destination port number used by cobaltstrike.exe when connecting to its C2 IP Address?**

Refer to screenshot above

> [!Success] Answer
81

> [!Question] 
**During our analysis, we found a process called cobaltstrike.exe. What is the parent process of cobaltstrike.exe?**

![image 75.png](/img/user/TryHackMe/THM_Images/3245775a65345cbd2d317f19266a1faa.png)

> [!Success] Answer
explorer.exe
