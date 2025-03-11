---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/log-fundamentals/","created":"2024-11-20T17:15:47.908-05:00","updated":"2025-03-11T00:32:59.278-04:00"}
---

# Task 2 - Type of Logs  

| Log Type         | Usage                                                                                                                                              | Example                                                                                                                                              |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| System Logs      | Helpful in troubleshooting running issues in the OS.  <br>These logs provide information on various operating system activities.                   | - System Startup and shutdown events<br>- Driver Loading events<br>- System Error events<br>- Hardware events                                        |
| Security Logs    | Help detect and investigate incidents.  <br>Provide information on the security-related activities in the system.                                  | - Authentication events<br>- Authorization events<br>- Security Policy changes events<br>- User Account changes events<br>- Abnormal Activity events |
| Application Logs | Specific events related to the application.  <br>Any interactive or non-interactive activity happening inside the application will be logged here. | - User Interaction events<br>- Application Changes, update, and error events                                                                         |
| Audit Logs       | System changes and user events.  <br>Helpful for compliance requirements and can play a vital role in security monitoring as well.                 | - Data Access events<br>- System Change events<br>- User Activity events<br>- Policy Enforcement events                                              |
| Network Logs     | Network’s outgoing and incoming traffic.  <br>Crucial in troubleshooting network issues and can also be handy during incident investigations.      | - Incoming and outgoing Network Traffic events<br>- Network Connection and firewall Logs                                                             |
| Access Logs      | Access to different resources.  <br>Can be of different types, providing us with information on their access.                                      | - Webserver Access Logs<br>- Database Access Logs<br>- Application Access Logs<br>- API Access Logs                                                  |

> [!Question]
> **Which type of logs contain information regarding the incoming and outgoing traffic in the network?** 

> [!Success] Answer
> Network Logs

> [!Question]
> **Which type of logs contain the authentication and authorization events?** 

> [!Success] Answer
> Security Logs  

# Task 3 - Types of Incidents

Logs in general are separated into set categories, for windows its,

| Application | Applications running in windows is logged into this file.<br><br>Information includes errors, warnings, compatibility issues, etc                                                                      |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| System      | Information related to these operations related to the OS is logged in the System log file.<br><br>Sriver issues, hardware issues, system startup and shutdown information, services information, etc. |
| Security    | Logs all security-related activities, including user authentication, changes in user accounts, security policy changes, etc.                                                                           |

Windows has event viewer to go over logs.

Exercise, to find logs of a compromised system to answer questions.

> [!Question]
> **What is the name of the last user account created on this system?** 

Went to event viewer and went to "Security"

![Exported image](/img/user/TryHackMe/THM_Images/b3d017a2e3dcabafe1035f770ab5b8ad.png)  

Filtered by the log event code "4720"

![Exported image](/img/user/TryHackMe/THM_Images/ea8310210f64129b6aa3f9d4ca437923.png)  

Found the latest event, and clicked on it to see that the name was being created, "hacked".
 
> [!Success] Answer
> hacked

> [!Question]
> **Which user account created the above account?** 

Refer to above screenshot

> [!Success] Answer
> Administrator

> [!Question]
> **On what date was this user account enabled?** 

Refer to above screenshot

> [!Success] Answer
> 6/7/2024

> [!Question]
> **Did this account undergo a password reset as well?** 

Had to filter by another event code to see if there was an attempt, used the event code 4724

![Exported image](/img/user/TryHackMe/THM_Images/beb1254c7265d2e52829c050571ff7cb.png)  

We see that there was an event of a password reset associated with this account

> [!Success] Answer
> Yes
              
# Task 4 - Web Server Access Logs Analysis

- Linux command line uses for viewing logs
	- **Cat**
		- Displays contents of log file
			- `Cat access.log`
			![Exported image](/img/user/TryHackMe/THM_Images/1bb99d9f9a22e8a0935358d1061eeab3.png)
		- Can combine results of multiple files in one command
			- `Cat access1.log access2.log > combinedAccess.log`
			![Exported image](/img/user/TryHackMe/THM_Images/3140702b008a56f0766047f7d42f22ce.png)
	- **Grep**
		- Searches for strings and patterns inside log files
			- `Grep "192.167.1.1" access.log`
			![Exported image](/img/user/TryHackMe/THM_Images/571f278fed65a6491568afa9a95e7c30.png)
	- **Less**
		- Good for handling multiple log files, view one page at a time
			- `Less access.log`
			![Exported image](/img/user/TryHackMe/THM_Images/fd589d6c48dd56eda6ed792e7aed2399.png)
		- "Spacebar" for next page, "b" for previous page
		- Can search with "/" followed by the pattern to search for
			- "n" for next occurrence, "N" for previous occurrence

Given web server log access file, view it to answer the questions below
![Exported image](/img/user/TryHackMe/THM_Images/75567b37e94b7b465195fa4f298c2ea7.png)

> [!Question]
> **What is the IP which made the last GET request to URL: “/contact?** 

![Exported image](/img/user/TryHackMe/THM_Images/5c817fec7831c71eccf88c5139d1037d.png)  

> [!Success] Answer
> 10.0.0.1

> [!Question]
> **When was the last POST request made by IP: “172.16.0.1”?** 

![Exported image](/img/user/TryHackMe/THM_Images/831f24ad460f1a0e73b2bd5fd8ebac85.png)  

> [!Success] Answer
> 06/Jun/2024:13:55:44

> [!Question]
> **Based on the answer from question number 2, to which URL was the POST request made?** 

Refer to screenshot above

> [!Success] Answer
> /contact    

