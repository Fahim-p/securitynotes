---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/offensive-security-intro/","created":"2024-12-03T17:33:00.000-05:00","updated":"2025-03-09T16:38:29.859-04:00"}
---

# Task 1 - What is Offensive Security?

> [!Question] 
> **1. What involves simulating a hacker's actions to find vulnerabilities and gain unauthorized access?**

> [!Success] Answer
> Offensive Security
# Task 2 - Hacking your first machine?

Went to the website "fakebank.thm" to get to this webpage, this is our target website.

![image1.png](/img/user/TryHackMe/THM_Images/acf96107ebcdb83fcf1bec8f941ca9f5.png)
    
- Went to terminal and used gobuster (directory scanner) with the command,
	- `gobuster -u -w wordlist.txt dir`
		- u stands for website,
		- -w stands for wordlist to use

![image2.png](/img/user/TryHackMe/THM_Images/6a7537a4e7ae499408851abefd0fcf8b.png)
    
We look for results that end with the status 200, meaning its valid.

![image3.png](/img/user/TryHackMe/THM_Images/5c915fd54d201c926df92e9260ef2972.png)
    
We can use the directory name "bank-transfer" as a page to search for in the search address bar with the Fake bank website. Doing so leads us to this webpage

![image4.png](/img/user/TryHackMe/THM_Images/58fd67157772bc9c263f5ecac8ec532b.png)
    
We follow the instructions provided to transfer money from one bank account to ours.

![image5.png](/img/user/TryHackMe/THM_Images/96e7d0c66f513b968763ba069a1a7480.png)

![image6.png](/img/user/TryHackMe/THM_Images/e88db595d8983a5c06c666d7d5795f33.png)
    
Doing so gives us the flag.

![image7.png](/img/user/TryHackMe/THM_Images/5a3bfd8f1ea05cda0f35c8e7e70c24ff.png)

> [!Question] 
**Above your account balance, you should now see a message indicating the answer to this question. Can you find the answer you need?**

> [!Success] Answer
BANK-HACKED