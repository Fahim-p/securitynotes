---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/gobuster/","created":"2024-11-04T16:50:31.208-05:00","updated":"2025-03-11T00:32:59.160-04:00"}
---

# Task 3 - Gobuster Introduction

| Short Flag | Long Flag  | Description                                                                                                                           |
| ---------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| -t         | --threads  | Configures the number of threads to use for the scan. Default number of threads is 10. May be slow when using large wordlists.        |
| -w         | --wordlist | The flag configures a wordlist to use for iterating. Each wordlist entry is attached to the URL you included in the command.          |
|            | --delay    | Defines the amount of time to wait between sending requests. Can increase the delay between requests to seem like normal web traffic. |
|            | --debug    | This flag helps us to troubleshoot when our command gives unexpected errors.                                                          |
| -o         | --output   | This flag writes the enumeration results to a file we choose.                                                                         |

Example command,
```
gobuster dir -u "[http://www.example.thm/](http://www.example.thm/)" -w /usr/share/wordlists/dirb/small.txt -t 64
```

> [!Question]
> **What flag to we use to specify the target URL?** - **What command do we use for the subdomain enumeration mode?** 

> [!Success] Answer
> dns
 
> [!Question]
> **What command do we use for the subdomain enumeration mode?**

> [!Success] Answer
> -u  
# Task 4 - Use Case: Directory and File Enumeration

| Flag | Long Flag                | Description                                                                                                                      |
| ---- | ------------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| -c   | --cookies                | Configures a cookie to pass along each request, such as a session ID.                                                            |
| -x   | --extensions             | Specifies which file extensions you want to scan for. E.g., .php, .js                                                            |
| -H   | --headers                | Configures an entire header to pass along with each request.                                                                     |
| -k   | --no-tls-validation      | Skips the process that checks the certificate when https is used. This causes an error during the TLS check.                     |
| -n   | --no-status              | Set this flag when you don’t want to see status codes of each response received. This helps keep the output on the screen clear. |
| -P   | password                 | Set this flag together with the --username flag to execute authenticated requests.                                               |
| -s   | --status-codes           | Can configure which status codes of the received responses you want to display, such as 200, or a range like 300-400.            |
| -b   | --status-codes-blacklist | Allows you to configure which status codes of the received responses you don’t want to display. Overrides the -s flag.           |
| -U   | --username               | Set this flag together with the --password flag to execute authenticated requests.                                               |
| -r   | --followredirect         | Configures Gobuster to follow the redirect that it received as a response to the sent request.                                   |

Example command to enumerate specific file types,
```
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .php,.js 
```

> [!Question]
> **Which flag do we have to add to our command to skip the TLS verification? Enter the long flag notation?**

> [!Success] Answer
> --no-tls-validation

> [!Question]
> **Enumerate the directories of [www.offensivetools.thm](http://www.offensivetools.thm). Which directory catches your attention?**
> 

Used the command, 
```
gobuster dir -u "[http://www.offensivetools.thm](http://www.offensivetools.thm)" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 64
```

![Exported image](/img/user/TryHackMe/THM_Images/8a1caa03f5207c9b24aa9daae7af2046.png)  

Of the directories listed, the one that caught my attention was "/secret"

> [!Success] Answer
> secret

> [!Question]
> **Continue enumerating the directory found in question 2. You will find an interesting file there with a .js extension. What is the flag found in this file?** 

Used the command,
```
gobuster dir -u "[http://www.offensivetools.thm/secret](http://www.offensivetools.thm/secret)" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 64 -x .js
```

![Exported image](/img/user/TryHackMe/THM_Images/7af25f584a473ac4a99519ce2103c384.png)  
Went to the file listed in the directory through the web address

![Exported image](/img/user/TryHackMe/THM_Images/8379263b7d050829ac9fc75f589c50c5.png)  

> [!Success] Answer
> THM{ReconWasASuccess}
# Task 5 - Use Case: Subdomain Enumeration

| Flag | Long Flag    | Description                                                                       |
| ---- | ------------ | --------------------------------------------------------------------------------- |
| -c   | --show-cname | Show CNAME Records (cannot be used with the -i flag).                             |
| -i   | --show-ips   | Including this flag shows IP addresses that the domain and subdomains resolve to. |
| -r   | --resolver   | This flag configures a custom DNS server to use for resolving.                    |
| -d   | --domain     | This flag configures the domain you want to enumerate.                            |

Example command
```
    gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```

- Make sure to enumerate for subdomains since they could still have vulnerabilities that are not patched compared to top domain
	- if THM owns tryhackme.thm and mobile.tryhackme.thm, there may be a vulnerability in mobile.tryhackme.thm that is not present in tryhackme.thm.

> [!Question]
> **Apart from the dns keyword and the -w flag, which shorthand flag is required for the command to work?**

> [!Success] Answer
> -d

> [!Question]
> **Use the commands learned in this task, how many subdomains are configured for the offensivetools.thm domain?** 

Used the command, 
```
`gobuster dns -d offensivetools.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt`
```

![Exported image](/img/user/TryHackMe/THM_Images/988f6b042bd6639fc49223f6573b72e3.png)  

> [!Success] Answer
> 4
# Task 6 - Use Case: Vhost Enumeration

| Short Flag | Long Flag         | Description                                                                                           |
| ---------- | ----------------- | ----------------------------------------------------------------------------------------------------- |
| -u         | --url             | Specifies the base URL (target domain) for brute-forcing virtual hostnames.                           |
|            | --append-domain   | Appends the base domain to each word in the wordlist (e.g., word.example.com).                        |
| -m         | --method          | Specifies the HTTP method to use for the requests (e.g., GET, POST).                                  |
|            | --domain          | Appends a domain to each wordlist entry to form a valid hostname (useful if not provided explicitly). |
|            | --exclude-length  | Excludes results based on the length of the response body (useful to filter out unwanted responses).  |
| -r         | --follow-redirect | Follows HTTP redirects (useful for cases where subdomains may redirect).                              |

- Example command    
```
    gobuster vhost -u "[http://10.10.123.14](http://10.10.123.14)" --domain example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain --exclude-length 250-320
```

- Virtual hosts are different websites on same machine
    - IP-based, not subdomains

> [!Question]
> **Use the commands learned in this task to answer the following question: How many vhosts on the offensivetools.thm domain reply with a status code 200?** 

Used the command, 

```
gobuster vhost -u "[http://10.10.123.14](http://10.10.123.14)" --domain offensivetools.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain --exclude-length 250-320
```

![Exported image](/img/user/TryHackMe/THM_Images/3921ab7509c71ff9d9553aeea6a4a1c1.png)  

> [!Success] Answer
> 4