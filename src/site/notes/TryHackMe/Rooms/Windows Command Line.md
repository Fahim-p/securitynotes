---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/windows-command-line/","created":"2024-12-09T18:38:00.000-05:00","updated":"2025-03-12T00:21:28.744-04:00"}
---

# Task 2 - Basic System Information

**set**, Checks path from command line
	
![image1 5.png](/img/user/TryHackMe/THM_Images/ff3cdf910f7363b96c20f7ce83104039.png)

**ver**, Shows OS version

![image2 5.png](/img/user/TryHackMe/THM_Images/28d8200dbcfc0341dd369de9666d2552.png)

**systeminfo**, List various information about system
        
![image3 5.png](/img/user/TryHackMe/THM_Images/51b229a65df4c3912d6b4fbefdb602f8.png)
        
- **more**, Used as a way to pipe through information to better view it
- **help**, Provides information for specific command
- **cls**, Clears command prompt screen

> [!Question] 
**What is the OS version of the Windows VM?**

> [!done] Answer
10.0.20348.2655

> [!Question] 
**What is the hostname of the Windows VM?**

![image5 5.png](/img/user/TryHackMe/THM_Images/340ac65f1412da31bd69ea0b4754fd64.png)

> [!done] Answer
WINSRV2022-CORE
# Task 3 - Network Troubleshooting

- **ipconfig**, Shows network configuration like ip address, subnet mask, and gateway
	- Use **/all** flag to get more info
        
![image6 5.png](/img/user/TryHackMe/THM_Images/972a142b9654b4f480f906ab3c9f3454.png)
        
- **ping**,  Shows if a server can access another server on the internet
- **tracert**, Traces network route from beginning node to destination

- **Nslookup**, Looks up a host/domain, returns IP address
        
![image7 5.png](/img/user/TryHackMe/THM_Images/07385cbcdb2286558a2ff56d4b6c6e42.png)
        
**Netstat**, Displays current network connections and listening ports
        
![image8 3.png](/img/user/TryHackMe/THM_Images/580c9d3c86e1a68c7757ebd8a6e0bc2e.png)
        
**Netstat -abon**
    
| -a  | displays all established connections and listening ports                         |
| --- | -------------------------------------------------------------------------------- |
| -b  | shows the program associated with each listening port and established connection |
| -o  | reveals the process ID (PID) associated with the connection                      |
| -n  | uses a numerical form for addresses and port numbers                             |
    
![image9 3.png](/img/user/TryHackMe/THM_Images/688aa6d1a278114fa73f664d6920f6d5.png)
    
> [!Question] 
**Which command can we use to look up the server’s physical address (MAC address)?**

> [!done] Answer
ipconfig /all

> [!Question] 
**What is the name of the process listening on port 3389?**

![image10 2.png](/img/user/TryHackMe/THM_Images/c53ef35710f99c5b58375724c38aa7de.png)

> [!done] Answer
TermService

> [!Question] 
**What is the IP address of your gateway?**

![image11 2.png](/img/user/TryHackMe/THM_Images/1a455f3f5ca5850581a44c4b025ebf41.png)

> [!done] Answer
10.10.0.1

# Task 4 - File and Disk Management

**cd**, No parameters shows current drive and directory
- Can change directories by giving it a parameter of a target directory
- **Cd ..**, Goes up one level
        
![image12 2.png](/img/user/TryHackMe/THM_Images/3d1956454a6c92ee69ce3d2b28a479bc.png)

**dir**, View child directories
- **/a** flag, Shows hidden and system files
- **/s** flag,  Display files in current directory and subdirectories

![image13 1.png](/img/user/TryHackMe/THM_Images/0d87cb38fa37c018eb41f6129fa17b89.png)
        
**Tree**, Visually represents child directories and subdirectories

![image14 1.png](/img/user/TryHackMe/THM_Images/421cfe4aad02b5517cc6309f9a29813c.png)

**Mkdir**, Makes a directory

![image15 1.png](/img/user/TryHackMe/THM_Images/ecbbe57c627ba6030b9d5bb619be206c.png)

**rmdir**, Removes a directory

![image16 1.png](/img/user/TryHackMe/THM_Images/aa0c77ca41fd3e6b83234adf03abe17d.png)

**type**, Views text files on screen

**copy**, Copy files from one location to another
        
![image17 1.png](/img/user/TryHackMe/THM_Images/907f68d2cb9cab7e9c453f017dffc694.png)
        
**move**, Moves files with it

![image18 1.png](/img/user/TryHackMe/THM_Images/fe4efa485b0c2165af19c5486ad3fc5f.png)
        
- **Del / erase**, Deletes a file

- Refer to multiple files using *
	- Example, `copy *.md C:\Markdown`
	- Copies all files with .md extension to the C:\Markdown directory

> [!Question] 
**What are the file’s contents in C:\Treasure\Hunt?**

![image19 1.png](/img/user/TryHackMe/THM_Images/e61fe1969524893b95d91b2be141427a.png)

> [!done] Answer
THM{CLI_POWER}

# Task 5 - Task and Process Management

**Tasklist**, Lists running processes like task manager
- `/?` Flag
	- Checks all available filters

![image20 1.png](/img/user/TryHackMe/THM_Images/6268b4300bd518a890814b18e5f00e5c.png)

- Example, search for tasks related to sshd.exe
	- `Tasklist /FI "imagename eq sshd.exe"`
		- /FI is used to set the filter image name equals sshd.exe.

![image21 1.png](/img/user/TryHackMe/THM_Images/cd825cfee1d9a2a28a8d00d5f86e08d1.png)
            
- **Taskkill**
	- Terminate any task with the PID
	- Example, `taskkill /PID 4567`

> [!Question] 
**What command would you use to find the running processes related to notepad.exe?**

> [!done] Answer
tasklist /FI "imagename eq notepad.exe"

> [!Question] 
**What command can you use to kill the process with PID 1516?**

> [!done] Answer
taskkill /PID 1516