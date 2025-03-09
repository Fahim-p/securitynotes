---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/linux-fundamentals-part-3/","created":"2024-12-03T19:25:00.000-05:00","updated":"2025-03-09T16:38:29.748-04:00"}
---

# Task 3 - Terminal Text Editors

**Nano**
- `Nano filename`
- Use "Ctrl" to with a corresponding letter to,
	- Search for text
	- Copy and Paste
	- Jump to a line number
	- Find out what line number you are on

![image1 4.png](/img/user/TryHackMe/THM_Images/7834386d80caf7024cfec65701fba24d.png)

**VIM**
- Customizable
	- Modify the keyboard shortcuts to be of your choosing
- Syntax Highlighting
	- Useful if you are writing or maintaining code, making it a popular choice for software developers
- Works on all terminals where nano may not be installed

![image2 4.png](/img/user/TryHackMe/THM_Images/eae209a63f90733745e115d0b2dde6e9.png)

> [!Question] 
**Edit "task3" located in "tryhackme"'s home directory using Nano. What is the flag?**

![image3 4.png](/img/user/TryHackMe/THM_Images/8cfa9fa6abbdc19b8d64b7c5e8a05fc6.png)

![image4 4.png](/img/user/TryHackMe/THM_Images/7c33f2aa7b5956441f0d5d1d6d0f88be.png)

> [!done] Answer: 
THM{TEXT_EDITORS}

# Task 4 - General/Useful Utilities

- **Wget**, Downloads files from the web via HTTP
- **SCP**
	- Secure copy, transfer files from host securely
	- Transfers between two computers using SSH
	- Copy files & directories from your current system to a remote system
	- Example, `scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt`
		- Important.txt, name of file on local system
		- Ubuntu, user on the remote system
		- 192.168.1.30, IP address of remote system
		- Transferred.txt, name of file to be stored on remote system
	- Vice versa
	- Example, `scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt`
		- Ubuntu, user on the remote system
		- 192.168.1.30, IP address of remote system
		- documents.txt, name of file on remote system
		- notes.txt, name of file to be stored on local system
- **WEB**
	- Ubuntu come with python3, with a module called "HTTPServer"
	- Allows other computers to download files from it using "curl" or "wget"
	- Can start it with,

```Bash
Python3 -m http.server
```

- No way to index

> [!Task] 
**Use Python 3's "HTTPServer" module to start a web server in the home directory of the "tryhackme" user on the deployed instance.**

![image5 4.png](/img/user/TryHackMe/THM_Images/d03624d46005ec12666dc1ec6b66116b.png)

> [!Question] 
**Download the file onto the TryHackMe AttackBox. Remember, you will need to do this in a new terminal. What are the contents?**

![image6 4.png](/img/user/TryHackMe/THM_Images/71a05b61a4f103b4e4fbdb885953c857.png)

![image7 4.png](/img/user/TryHackMe/THM_Images/ddc43aa914bb343fec12ffe626de8dea.png)

> [!done] Answer
THM{WGET_WEBSERVER}

> [!Task] 
**Use Ctrl + C to stop the Python3 HTTPServer module once you are finished**

![image8 2.png](/img/user/TryHackMe/THM_Images/2d3cdff09a2b3896397adaf3d7dc7226.png)
# Task 5 - Processes 101

**PID**, Process ID
- Increments for order in which the process starts

**ps**, Provides list of running processes
- Gives,
	- Status code
	- Session that its running in
	- CPU usage time
	- Name of actual program being used

![image9 2.png](/img/user/TryHackMe/THM_Images/edc76e66c59b0f37174439d3dd2cb859.png)
        
**Ps -aux**, See processes run by other users and those that don't run from a session (i.e. system processes)
	
![image10 1.png](/img/user/TryHackMe/THM_Images/551b9c4b2104d0e9640a0890e9bc78a8.png)
	
**Top**, Real time statistics about processes running on system
- Refreshes every 10 seconds or when scrolling through

![image11 1.png](/img/user/TryHackMe/THM_Images/6e4193643bb954fe8bc820b6ee08635c.png)
        
- **Terminating processes**
	- `Kill`
		- Terminates given process, uses PID
		- Example, kill 1337
	- `SIGTERM`
		- Kill the process, but allow it to do some cleanup tasks beforehand
	- `SIGKILL`
		- Kill the process - doesn't do any cleanup after the fact
	- `SIGSTOP`
		- Stop/suspend a process
- **Starting processes**
	- OS uses namespaces to split up resources on computer
		- Great for security, isolates processes from each other
		- Only those in same namespace will be able to see each other

**Systemd**
- First processes that's started on boot
- Programs/softwares will be a child process of it
	- Controlled by it, but will run as its own process

![image12 1.png](/img/user/TryHackMe/THM_Images/c471d763279b2fa8e4513fe336868e65.png)

- **Systemctl**
	- Allows for interaction with systemd process
	- Format of `systemctl [option] [service]`
	- Example, `systemctl start apache2`
	- Four options
		- Start
		- Stop
		- Enable
		- Disable
	- Processes can run in the foreground or background
		- Great for copying files since we can run it in the background and continue on without waiting for it to be done
		- **Ctrl-Z**
			- Backgrounds a process
			- Also pauses a script execution/command
			- Can still view the process running with **ps aux**

![image13.png](/img/user/TryHackMe/THM_Images/62727c8132d573a74bbdb4a4c1074236.png)

**Fg**
- Brings backgrounded processes to the foreground

![image14.png](/img/user/TryHackMe/THM_Images/348b1c2875b738975f9048a041474330.png)

![image15.png](/img/user/TryHackMe/THM_Images/6403ddef10be1f55fbf08c249ff2aed7.png)

> [!Question] 
**If we were to launch a process where the previous ID was "300", what would the ID of this new process be?**

> [!done] Answer
301

> [!Question] 
**If we wanted to cleanly kill a process, what signal would we send it?**

> [!Done] Answer
SIGTERM

> [!Question] 
**Locate the process that is running on the deployed instance (10.10.47.92). What flag is given?**

![image16.png](/img/user/TryHackMe/THM_Images/c89be58005bde2586bf90f0d19e6cfb9.png)

> [!Done] Answer
THM{PROCESSES}

> [!QUestion] 
**What command would we use to stop the service "myservice"?**

> [!Done] Answer
systemctl stop myservice

> [!Question] 
**What command would we use to start the same service on the boot-up of the system?**

> [!done] Answer
systemctl enable myservice

> [!question] 
**What command would we use to bring a previously backgrounded process back to the foreground?**

> [!done] Answer
fg

# Task 6 - Maintaining Your System: Automation

- Can automate tasks/actions after system has booted with Cron
	- Crontabs
		- Started during boot
		- Facilitates and manages Cron jobs
		- Recognised by the Cron process to execute each line step-by-step
		- Require 6 values

| Value | Description                               |
| ----- | ----------------------------------------- |
| MIN   | What minute to execute at                 |
| HOUR  | HOUR What hour to execute at              |
| DOM   | What day of the month to execute at       |
| MON   | What month of the year to execute at      |
| DOW   | DOW What day of the week to execute at    |
| CMD   | The actual command that will be executed. |

- Example, for backing up a document every 12 hours,
	- `0 */12 * * * cp -R /home/cmnatic/Documents /var/backups/`
- Supports wildcards *
	- Used when we don't need to specify specific value for any fields
- Websites to help out,
	- [https://crontab-generator.org](https://crontab-generator.org/)
	- [https://crontab.guru](https://crontab.guru/)
- Can be edited with `crontab -e`

> [!Question] 
**When will the crontab on the deployed instance (10.10.47.92) run?**

![image17.png](/img/user/TryHackMe/THM_Images/0cebb891cf7015c5c1d168594219d3fa.png)

![image18.png](/img/user/TryHackMe/THM_Images/f24b554e49c78061dbf4dc9d1ce94098.png)

> [!Done] Answer
@reboot

# Task 7 - Maintaining Your System: Package Management

- Developers submit their software to an "apt" repository
	- If allowed, then it'll be fully released to the public

![image19.png](/img/user/TryHackMe/THM_Images/7fd3823400531a57205eb295e552c71f.png)

Files serve as gateway/registry

![image20.png](/img/user/TryHackMe/THM_Images/4d02e395a10f0d60a2f205fd8b25f880.png)
    
- Can add community repositories through the `add-apt-repository` command
- **Apt**
	- Command used to install and manage software
	- Part of package management software called "apt"
	- Whenever we update our system, all repositories that we add through apt gets checked for update as well
	- Example of manually installing through APT, using Sublime text
	- **GPG keys**
		- Used as a way of checking integrity of file
		- Download the GPG key and use apt-key to trust it:

```Bash
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
```

- Add Sublime Text 3's repository to our apt sources list.
	- A good practice is to have a separate file for every different community/3rd party repository that we add.
	- Create a file named sublime-text.list in `/etc/apt/sources.list.d` and enter the repository information like so:

![image21.png](/img/user/TryHackMe/THM_Images/2d571962d65b4bc653ae0105df99f61f.png)
        
Use text editor to add & save the Sublime Text 3 repository into this newly created file:

![image22.png](/img/user/TryHackMe/THM_Images/ec748b225bbc7a1004435b01343f60e3.png)
    
- Once updated, we can proceed to install the software that we have trusted and added to apt
	- `apt install sublime-text`
	- Can uninstall with `add-apt-repository --remove`
	- Then can use `apt remove`
		- Can use package installers like dpkg instead of apt as well
# Task 8 - Maintaining Your System: Logs

- Logs
	- Located in /var/log directory
	- Contains logging information for apps and services running on system
	- OS manages them automatically through "rotating"
	- Great way to monitor health of system

> [!task] 
**Look for the apache2 logs on the deployable Linux machine**

![image23.png](/img/user/TryHackMe/THM_Images/de91780d965e7139e7fa21c2b95be2c4.png)

> [!question] 
**What is the IP address of the user who visited the site?**

![image24.png](/img/user/TryHackMe/THM_Images/2f951caaec0e8bd5468c3278adb91e38.png)

> [!done] Answer
10.9.232.111

> [!question] 
**What file did they access?**

![image25.png](/img/user/TryHackMe/THM_Images/3ae6458efa93bcebda770de438066c80.png)

> [!done] Answer
catsanddogs.jpg