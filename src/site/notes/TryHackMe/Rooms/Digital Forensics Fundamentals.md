---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/digital-forensics-fundamentals/","created":"2024-11-17T17:24:39.640-05:00","updated":"2025-03-11T00:32:59.135-04:00"}
---

# Task 1 - Introduction to Digital Forensics

- Branch of forensics that investigates cyber crimes
	- Application of methods and procedures to investigate and solve crimes
- Cyber Crime
	- Criminal activity conducted on or used a digital device 

> [!Question]
> **Which team was handed the case by law enforcement?** 

> [!Success] Answer
> Digital Forensics
# Task 2 - Digital Forensics Methodology

- NIST defines the framework for digital forensics into 4 phases
	- **Collection**
		- Identify all devices which data can be collected from
		- Ensure original data is not tampered with
		- Document collected item details
	- **Examination**
		- Needs to be filtered, data of interest to be extracted
		- Meant to filter particular data for analysis
	- **Analysis**
		- Analyze data by correlating it with multiple pieces of evidence to draw conclusions
		- Extract activities relevant to the case chronologically
	- **Reporting**
		- Prepare report with investigations methodology and detailed findings from collected evidence
		- May give recommendations
		- Present to law enforcement and executive management
- **Types of digital forensics**

| Computer forensics: | Investigating computers, the devices most commonly used in crimes.                                                                                   |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| Mobile forensics:   | Investigating mobile devices and extracting evidence such as call records, text messages, GPS locations, and more.                                   |
| Network forensics:  | Investigation beyond individual devices, includes the whole network. The majority of the evidence found in networks is the network traffic logs.     |
| Database forensics: | Investigates any intrusion into these databases that results in data modification or exfiltration.                                                   |
| Cloud forensics:    | Investigating data stored on cloud infrastructure. Sometimes gets tricky for the investigators as there is little evidence on cloud infrastructures. |
| Email forensics:    | Investigating emails to determine whether they are part of phishing or fraudulent campaigns.                                                         |

> [!Question]
> **Which phase of digital forensics is concerned with correlating the collected data to draw any conclusions from it?** 

> [!Success] Answer
> Analysis

> [!Question]
> **Which phase of digital forensics is concerned with extracting the data of interest from the collected evidence?** 

> [!Success] Answer
> Examination
# Task 3 - Evidence Acquisition

- **Proper authorization**
	- Need to get proper authorization before collecting data according to limits of the law
	- Forensic evidence contains private and sensitive data of organization/individual
- **Chain of custody**
	- Formal document containing all details of the evidence
		- Description of the evidence (name, type).
		- Name of individuals who collected the evidence.
		- Date and time of evidence collection.
		- Storage location of each piece of evidence.
		- Access times and the individual record who accessed the evidence.
	- Proper trail of evidence, helps preserve it
	- Proves integrity and reliability of evidence admitted in court
- **Use of Write Blockers**
	- Used to ensure that the tasks of the forensic workstation does not alter timestamps of the files on the hard drive
	- Blocks any evidence alteration actions 

> [!Question]
> **Which tool is used to ensure data integrity during the collection?** 

> [!Success] Answer
> Write Blocker

> [!Question]
> **What is the name of the document that has all the details of the collected digital evidence?** 

> [!Success] Answer
> Chain of Custody
# Task 4 - Windows Forensics

- Two categories of forensic images of Windows OS are taken
	- Bit-by-bit copies of the whole OS
	- **Disk Image**
		- Contains all data present on storage device
		- Non-volatile
	- **Memory Image**
		- Contains data inside OS's RAM
		- Volatile, to be prioritized first
- Popular tools for disk and memory image acquisition/analysis
	- **FTK Imager**
		- User-friendly graphical interface
		- Analyze contents of disk image
		- Both acquisition and analysis
	- **Autopsy**
		- Open-source platform
		- Import disk image into tool to get extensive analysis of the image
		- Keyword search, deleted file recovery, file metadata, extension mismatch detection, etc.
	- **Dumpit**
		- Takes memory image in different formats using CMD
	- **Volatility**
		- Open-source tool for analyzing memory images
		- Supports variety of OSs

> [!Question]
> **Which type of forensic image is taken to collect the volatile data from the operating system?** 

> [!Success] Answer
> Memory Image
# Task 5 - Practical Exercise of Digital Forensics

Been given a pdf and image, to be analyzed for evidence to save our cat, Gado.

![Exported image](/img/user/TryHackMe/THM_Images/77b3a4de8acc5be88b1885eb26f9bd91.png)

> [!Question] 
> **Using pdfinfo, find out the author of the attached PDF file, ransom-letter.pdf.** 

![Exported image](/img/user/TryHackMe/THM_Images/9dc4832f996496ae1fd346d95d2b95c6.png)  

> [!Success] Answer
> Ann Gree Shepherd

> [!Question]
> **Using exiftool or any similar tool, try to find where the kidnappers took the image they attached to their document. What is the name of the street?** 

![Exported image](/img/user/TryHackMe/THM_Images/18782bc698086ea3d926b01e81b0cf2e.png)  

Output goes on for a while, found this part about the GPS Position

![Exported image](/img/user/TryHackMe/THM_Images/87e4e763ed182805fc702263a9bb0668.png)  

Put it into google as, 51°30'51.9"N 0°05'38.7"W, got the street, Milk St (street)

![Exported image](/img/user/TryHackMe/THM_Images/5be45e730b96abe64861cd0c328487b4.png)  

> [!Success] Answer
> Milk Street

> [!Question]
> **What is the model name of the camera used to take this photo?** 

From the exiftool command, found a section that mentions the Camera Model Name

![Exported image](/img/user/TryHackMe/THM_Images/edbe9396525a46011b1211ddacb16073.png)  

> [!Success] Answer
> Canon EOS R6
