---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/nmap-the-basics/","created":"2024-10-25T15:46:36.380-04:00","updated":"2025-03-12T00:21:28.540-04:00"}
---


| **Option**                                                      | **Explanation**                                                                                    |
| --------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| -                                                               | Scan IP addresses in a range, example, can write 192.168.0.1-10                                    |
| /                                                               | Scan entire subnet                                                                                 |
| Hostname                                                        | Target by hostname, example, tryhackme.thm                                                         |
| -sL                                                             | List scan – list targets without scanning                                                          |
| **Host Discovery**                                              |                                                                                                    |
| -sn                                                             | Ping scan – host discovery only                                                                    |
| **Port Scanning**                                               |                                                                                                    |
| -sT                                                             | TCP connect scan – complete three-way handshake                                                    |
| -sS                                                             | TCP SYN – only first step of the three-way handshake                                               |
| -sU                                                             | UDP Scan                                                                                           |
| -F                                                              | Fast mode – scans the 100 most common ports                                                        |
| -p[range]                                                       | Specifies a range of port numbers – -p- scans all the ports                                        |
| -Pn                                                             | Treat all hosts as online – scan hosts that appear to be down                                      |
| **Service** **Detection**                                       |                                                                                                    |
| -O                                                              | OS detection                                                                                       |
| -sV                                                             | Service version detection                                                                          |
| -A                                                              | OS detection, version detection, and other additions                                               |
| **Timing**                                                      |                                                                                                    |
| -T<0-5>                                                         | Timing template – paranoid (0), sneaky (1), polite (2), normal (3), aggressive (4), and insane (5) |
| --min-parallelism <numprobes> and --max-parallelism <numprobes> | Minimum and maximum number of parallel probes                                                      |
| --min-rate <number> and --max-rate <number>                     | Minimum and maximum rate (packets/second)                                                          |
| --host-timeout                                                  | Maximum amount of time to wait for a target host                                                   |
| **Real-time output**                                            |                                                                                                    |
| -v                                                              | Verbosity level – for example, -vv and -v4                                                         |
| -d                                                              | Debugging level – for example -d and -d9                                                           |
| **Report**                                                      |                                                                                                    |
| -oN <filename>                                                  | Normal output                                                                                      |
| -oX <filename>                                                  | XML output                                                                                         |
| -oG <filename>                                                  | grep-able output                                                                                   |
| -oA <basename>                                                  | Output in all major formats                                                                        |
# Task 2 - Host Discovery - Who Is Online

> [!Question]
> **What is the last IP address that will be scanned when your scan target is 192.168.0.1/27**

![Pasted image 20250204152756.png](/img/user/TryHackMe/THM_Images/239e36a4128822f77f32d987d609a135.png)

> [!Success] Answer
> 192.168.0.31
# Task 3 - Port Scanning: Who is Listening

> [!Question]
> **How many TCP ports are open on the target system at 10.10.117.211?** 

![Exported image](/img/user/TryHackMe/THM_Images/567583e4fd9a100d8eb374798b335176.png)

> [!Success] Answer
> 26

> [!Question]
>  **Find the listening web server on 10.10.117.211 and access it with your browser. What is the flag that appears on its main page?**
 
![Exported image](/img/user/TryHackMe/THM_Images/664f20ad6f643a9db10ca3a87fabbaee.png)  

> [!Success] Answer
> 192.168.124.148
# Task 4 - Version Detection: Extract More Information
   
> [!Question] Question
**What is the name and detected version of the web server running on 10.10.117.211?** 

![Exported image](/img/user/TryHackMe/THM_Images/ce162c8c68277b2a3fd7b844c41db2e0.png)  

> [!Success] Answer
> lighttpd 1.4.74
# Task 5 - Timing: How Fast is Fast

> [!Question]
> **What is the non-numeric equivalent of -T4?** 
> 

> [!Success] Answer
> -T aggressive
# Task 6 - Output: Controlling What You See

> [!Question]
> **What option must you add to your nmap command to enable debugging?** 

> [!Success] Answer
> -d

# Task 7 - Conclusion and Summary

> [!Question]
> **What kind of scan will Nmap use if you run nmap 10.10.117.211 with local user privileges?** 

> [!Success] Answer
> Connect Scan