---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/introduction-to-siem/","created":"2024-11-20T18:16:23.906-05:00","updated":"2025-03-12T00:21:28.378-04:00"}
---

# Task 2 - Network Visibility through SIEM

- **Host-Centric** Log Sources
	- A user accessing a file
	- A user attempting to authenticate.
	- A process Execution Activity
	- A process adding/editing/deleting a registry key or value.
	- PowerShell execution
- **Network-Centric** Log Sources
	- SSH connection
	- A file being accessed via FTP
	- Web traffic
	- A user accessing company's resources through VPN.
	- Network file sharing Activity
- **SIEM Importance**
	- Real-time log Ingestion
	- Alerting against abnormal activities
	- 24/7 Monitoring and visibility
	- Protection against the latest threats through early detection
	- Data Insights and visualization
	- Ability to investigate past incidents. 

> [!Question]
> **Is Registry-related activity host-centric or network-centric?** 

> [!Success] Answer
> Host-Centric

> [!Question]
> **Is VPN related activity host-centric or network-centric?** 

> [!Success] Answer
> Network-Centric
# Task 3 - Log Sources and Log Ingestion

- **Windows**
	- Event Viewer
		- Assigns unique ID to each log activity
		- Different logs are stored and can be viewed
- **Linux**
	- Common locations for /var/log
		- Httpd
		- Cron
		- Auth.log / secure
		- Kern
- **Web Server**
	- Apache related logs are stored on /var/log/apache or httpd
- **Log ingestion methods**
	- **Agent/Forwarder**
		- Agent (forward by splunk) is installed in endpoint
		- Captures set logs and sends it to SIEM server
	- **Syslog**
		- Protocol to collect various data
		- Sends real-time data to centralized destination
	- **Manual Upload**
		- User can input offline data for analysis
	- **Port-Forwarding**
	    - SIEM can listen on certain port
	    - Endpoints forward data to SIEM on listening port

> [!Question]
> **In which location within a Linux environment are HTTP logs stored?**     

> [!Success] Answer
> /var/log/httpd 

# Task 4 - Why SIEM

- Correlation between events from different log sources.
- Provide visibility on both Host-centric and Network-centric activities.
- Allow analysts to investigate the latest threats and timely responses.
- Hunt for threats that are not detected by the rules in place
- **SOC Analyst Responsibilities**
	- Monitoring and Investigating.
	- Identifying False positives.
	- Tuning Rules which are causing the noise or False positives.
	- Reporting and Compliance.
	- Identifying blind spots in the network visibility and covering them.    
# Task 5 - Analyzing Logs and Alerts

- **Dashboard**
	- Alert Highlights
	- System Notification
	- Health Alert
	- List of Failed Login Attempts
- **Correlation Rules**
	- Logical expressions set to be triggered
		- If a User gets 5 failed Login Attempts in 10 seconds
			- Raise an alert for Multiple Failed Login Attempts
- **Alert Investigation**
	- Analyst has to determine if alert is a true or false positive
	- Alert is False Alarm.
		- It may require tuning the rule to avoid similar False positives from occurring again.
	- Alert is True Positive.
		- Perform further investigation.
		- Contact the asset owner to inquire about the activity.
		- Suspicious activity is confirmed. Isolate the infected host.
		- Block the suspicious IP.

> [!Question]
> **Which Event ID is generated when event logs are removed?** 

> [!Success] Answer
> 104

> [!Question]
> **What type of alert may require tuning?** 

> [!Success] Answer
> False alarm
# Task 6 - Lab Work

Sample dashboard/events are displayed, then alerts are triggered,

![Exported image](/img/user/TryHackMe/THM_Images/b76106f2694a498878e807358a0f11c7.png)

> [!Question]
> **Click on Start Suspicious Activity, which process caused the alert?**   

![Exported image](/img/user/TryHackMe/THM_Images/7d2211f14bec4a43ed4c11bd9b351000.png)  
![Exported image](/img/user/TryHackMe/THM_Images/be414d1ed73a7b6f209e7d27359fa107.png)  

> [!Success] Answer
> cudominer.exe

> [!Question]
> **Find the event that caused the alert, which user was responsible for the process execution?**   

![Exported image](/img/user/TryHackMe/THM_Images/c13c0939df67ce718c9184a511037c09.png)  
![Exported image](/img/user/TryHackMe/THM_Images/0ddf24915379fd3b24d3b23cc673c4fb.png)  

> [!Success] Answer
 > chris.fort

> [!Question]
> **What is the hostname of the suspect user?** 

See screenshot above

> [!Success] Answer
> HR_02

> [!Question]
> **Examine the rule and the suspicious process; which term matched the rule that caused the alert?** 

Clicking on the event shows us the rule that triggers this alert

![Exported image](/img/user/TryHackMe/THM_Images/34c5ac1607469cf122a84d31dd805d24.png)  

> [!Success] Answer
> miner

> [!Question] 
> What is the best option that represents the event? Choose from the following,

![Exported image](/img/user/TryHackMe/THM_Images/f5ebac981b5a4988ebd920de5ba6ae75.png)  

> [!Success] Answer
> True-Positive

> [!Question]
> **What is the flag found after closing the alert?** 

![Exported image](/img/user/TryHackMe/THM_Images/4690c3095432a2ed938d9e74dbdd29a7.png)  

> [!Success] Answer
> THM{000_SIEM_INTRO}





         
