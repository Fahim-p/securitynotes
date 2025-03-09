---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/linux-fundamentals-part-1/","created":"2024-12-03T18:14:00.000-05:00","updated":"2025-03-09T16:38:29.720-04:00"}
---

# Task 4 - Running Your First Few Commands

- **Echo,** Output any text that we provide
- **Whoami**, Find out what user we're currently logged in as!

> [!Question] 
**If we wanted to output the text "TryHackMe", what would our command be?**

![image1 2.png](/img/user/TryHackMe/THM_Images/5fa375c3596b8b2927ce47b3f7b7d181.png)

> [!done] Answer: 
 `echo TryHackMe`

> [!question] 
**What is the username of who you're logged in as on your deployed Linux machine?**

![image2 2.png](/img/user/TryHackMe/THM_Images/1b66e272509100082e1768a4a0d5129e.png)

> [!done] Answer
tryhackme

# Task 5 - Interacting With the Filesystem!

- **ls**, Listing
- **Cd**, change directory
- **Cat**, Concatenate/output
- **Pwd**, print working directory

> [!Question] 
**On the Linux machine that you deploy, how many folders are there?**

![image3 2.png](/img/user/TryHackMe/THM_Images/71edf551b3cc70bfa126efcf5afd4f3f.png)

> [!done] Answer
4

> [!Question] 
**2. Which directory contains a file?**

![image4 2.png](/img/user/TryHackMe/THM_Images/822a8aad554b677156e0ab8982ac9209.png)

> [!done] Answer
Folder4

> [!question] 
**What is the contents of this file?**

![image5 2.png](/img/user/TryHackMe/THM_Images/3abf016424ccfa8ce54988ff4aebfa95.png)

> [!done] Answer
Hello World!

> [!Question] 
**Use the cd command to navigate to this file and find out the new current working directory. What is the path?**

![image6 2.png](/img/user/TryHackMe/THM_Images/265fcde578f41321d81960ca39a94533.png)

> [!done] Answer
/home/tryhackme/folder4

# Task 6 - Searching for Files

- **Find**
	- Can look recursively within directories for said files
        
		```Bash
		file -name passwords.txt
		```
        
	- Can use wildcards to find files that have certain extensions at the end
        
```Bash
		file -name *.txt
```
        
- **Grep**
	- Search for contents of files for specified values
		
		```Bash
		grep '81.143.211.90' access.log
		```


> [!Question]
**Use grep on "access.log" to find the flag that has a prefix of "THM". What is the flag?**

![image7 2.png](/img/user/TryHackMe/THM_Images/b205c5f858f16012c1a321334e088da0.png)

> [!done] Answer
THM{ACCESS}

# Task 7 - An Introduction to Shell Operators

- **&**
	- Run commands in the background of your terminal.
- **&&**
	- Combine multiple commands together in one line of your terminal.
- **>**
	- redirector - take the output from a command (such as using cat to output a file) and direct it elsewhere.
- **>>**
	- Same function of the > operator but appends the output rather than replacing (meaning nothing is overwritten).

> [!Question] 
**If we wanted to run a command in the background, what operator would we want to use?**

> [!done] Answer
&

> [!Question] 
**If I wanted to replace the contents of a file named "passwords" with the word "password123", what would my command be?**

> [!done] Answer
`echo password123 > passwords`

> [!question] 
**Now if I wanted to add "tryhackme" to this file named "passwords" but also keep "passwords123", what would my command be?**

> [!done] Answer
`echo tryhackme >> passwords`