---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/dast/","created":"2025-03-04T22:18:26.695-05:00","updated":"2025-03-11T00:32:59.114-04:00"}
---

# Task 2 - Dynamic Application Security Testing (DAST)

- Process of **testing a running instance of a web application for weaknesses and vulnerabilities.** 
	- **Black-box** approach where vulnerabilities are found just like a regular attacker would find them. 
	- Identifies vulnerabilities by trying to exploit them.
- **Does not worry about the inner workings** and focus on identifying vulnerabilities that an attacker would likely find. 
	- Results will point to vulnerabilities requiring prioritized attention as they are expected to be found without prior knowledge of the application.
- Does not replace other methods to find vulnerabilities in applications, but rather complements them. 
	- A secure development lifecycle will mix several techniques in order to provide a good enough vulnerability coverage.
- DAST can be performed in two ways:
	- **Manual DAST**
		- A security engineer will manually perform tests against an application to check for vulnerabilities.
		- Helps to find weaknesses that automated tools won't easily spot as they don't understand the application from a functional point of view.
		- Takes too much time. 
	- **Automatic DAST**
		- An automated tool will scan the web application for vulnerabilities.
		- Provides a quick way to run many tests against the target application without requiring human interaction.
	- Both are complementary and can be used at different stages of the SDLC. 
		- Best results to combine them rather than relying on either separately.
- **DAST in the SDLC**
	- Automated DAST is used during the test phases
		- Optimized for speed so developers can obtain feedback quickly 
		- Goal is to catch low-hanging fruit early.
	- Manual DAST is ran periodically to avoid slowing down the development process as a whole. 
		- It is usual to run manual scans weekly while applications are being developed
	- Can run a full-blown web application pen test when application is ready for production
- **DAST Pros and Cons**

| Pros                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Cons                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| - Finds vulnerabilities during runtime. This will include vulnerabilities that are specific to the deployment process, which can't be seen by analyzing code alone.<br>- Will find vulnerabilities like HTTP Request Smuggling, cache poisoning, and parameter pollution that won't be found using SAST.<br>- All apps are treated in a language-agnostic way.<br>- Reduced number of false positives as compared to SAST.<br>- Might be able to find some business logic flaws. | - May not cover specific situations that will only be triggered by specific use cases in your application.<br>- Some vulnerabilities may be harder to find using DAST, as compared to SAST.<br>- Some apps are difficult to be crawled. Modern applications heavily rely on JavaScript processing for the client-side. This makes it harder for DAST tools to traverse them.<br>- Won't be able to tell you how to remediate some vulnerabilities in detail, since they have no idea of the underlying code.<br>- Some types of scans might take lots of time to finish.<br>- You need a running application to do the testing. |

- DAST can be contextualized as a series of automated tests. A DAST tool will perform at least the two following tasks against the target website:
	- **Spidering/Crawling** 
		- The tool will navigate through the web app, trying to map the application and identify a list of pages and parameters that can be attacked.
	- **Vulnerability Scanning** 
		- The tool will try to launch attack payloads against the identified pages and parameters. Can customize attacks to include ones relevant to the target.


> [!Question]
>  **Is DAST a replacement for SAST or SCA? (Yea/Nay)?**

> [!Success] Answer
> Nay

> [!Question]
>  **What is the process of mapping an application's surface and parameters usually called?**

> [!Success] Answer
> Spidering/Crawling

> [!Question]
>  **Does DAST check the code of an application for vulnerabilities? (Yea/Nay)?**

> [!Success] Answer
> Nay

# Task 3 - Spiders and Crawlers

- **Spidering an app with ZAP**
	- First step is to map out all resources in our target web application to identify the scope of our analysis. 
	- **Spider**
		- Will navigate to a starting page provided and explore the website by following all the links it can detect.
		- Go to `Tools -> Spider`.
			- Need to specify a website as our starting point
				- **Recurse**
					- Spider the website for links recursively.
				- **Spider Subtree Only**
					- Limit the spidering to subfolders of the Starting Point URL.
				- **Show Advanced Options**
					- Enable the Advanced tab, where you can specify additional parameters to tune your spidering.
		- Once ran, it shows all URLS that the spider found in the "Sites" tab
			- Any item outside your starting page's URL is considered out-of-scope and won't be added to the list.
		- Links that are not directly embedded in the page's HTML code but is generated on-the-fly by using JavaScript on browser cannot be detected by ZAP. 
			- Regular spider in ZAP doesn't have a JavaScript engine, it has no way of finding that link.
	- **AJAX Spider**
		- Can leverage a real browser like Chrome to process any scripts attached to the website and retrieve the resulting HTML code. 
			- Parses links from the result of a browser processing the website. 
		- Guarantees that the result will match what a user will see if they use the same browser.
		- `Tools -> AJAX Spider` 
			- Configure a URL as a starting point and check the options you see fit. 
			- Browser selection
				- Headless options
					- Runs the selected browser without showing you its graphical interface


> [!Question]
>  **ZAP can run an AJAX spider by using browsers without a Graphical User Interface(GUI). What are these browsers called?**

> [!Success] Answer
> Headless

> [!Question]
>  **Analysing the Sites tab, what HTTP parameters can be passed to login.php using the POST method? (In alphabetical order and separated by commas)?**

Had to download ZAP Proxy first with the command `Sudo apt install zaproxy`

![](/img/user/TryHackMe/THM_Images/Screenshot 2025-03-09 140654.png)

Went to **Tools -> Spider** and put in the URL of the targeted server (http://10.10.190.118:8082/)

![](/img/user/TryHackMe/THM_Images/Screenshot 2025-03-09 141815.png)

![](/img/user/TryHackMe/THM_Images/Screenshot 2025-03-09 142049.png)

![](/img/user/TryHackMe/THM_Images/Screenshot 2025-03-09 142259.png)

> [!Success] Answer
> Pass, user

> [!Question]
>  **What other .php resource, besides nospiders-gallery.php was found by the AJAX spider but not by the regular spider?**

This time, opened up **AJAX spider**

![](/img/user/TryHackMe/THM_Images/Screenshot 2025-03-09 142325.png)

![](/img/user/TryHackMe/THM_Images/Screenshot 2025-03-09 142750.png)

Running the scan opened up the browser multiple times to crawl through the website.

![](/img/user/TryHackMe/THM_Images/Screenshot 2025-03-09 142816.png)

![](/img/user/TryHackMe/THM_Images/Screenshot 2025-03-09 142851.png)

> [!Success] Answer
> /view.php

# Task 4 - Scanning for Vulnerabilities

- **Configuring a Scan Policy in ZAP**
	- Crucial to customize what types of tests will be run against the application.
	- The more you fit your scanning profile to your web application 
		- Less time the scanner will spend sending irrelevant payloads
	- Since it's used in a white box setup, underlying technologies used to support application are known.
	- `Analyse -> Scan Policy Manager`
		- **Threshold**
			- Controls the verbosity of each category. 
			- Lower threshold means ZAP is more likely to report a vulnerability based on little information. 
				- More findings at the risk false positives. 
			- A higher threshold will indicate ZAP to only report findings with a high degree of certainty. 
				- Fewer results, but those are more likely confirmed. 
				- The risk of using higher thresholds is that it can result in false negatives
		- **Strength**
			- Controls how many tests are run for each category. 
			- Higher strength levels are likely to report additional findings at the cost of increased scan time
- Once policy is set, we can use it with our vulnerability scan to get results
- Once it's done, we can go to the `Alerts` section to see what was found,
	- Can see description of found vulnerabilities, request and responses used by ZAP to find it
	- Able to flag them for false positives or review them as legitimate

> [!Question]
>  **Will disabling some test categories help speed up the scanning phase? (Yea/Nay)**

> [!Success] Answer
> Yea

> [!Question]
>  **There should be two high-risk alerts in your scan results. One is Path Traversal. What's the name of the other one?**

Frist had to create a new specialized policy for scans just for this room.

Went to `Analyze -> Scan Policy Manager`

![](/img/user/TryHackMe/THM_Images/Screenshot 2025-03-09 143105.png)

![](/img/user/TryHackMe/THM_Images/Screenshot 2025-03-09 143124.png)

Given from the room are the details of our target machine

"
- **Operative System:** Linux
- **Web Server:** Apache 2.4
- **Programming Language:** PHP (No frameworks used)
- **Databases:** None
"

We can turn off certain scans like SQL injections or XSS to speed up scan time and lower resource usage.

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309144416.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309144427.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309144448.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309144501.png)

Went to `Tools -> Active Scan` and selected our starting point and newly created policy.

![](/img/user/TryHackMe/THM_Images/Screenshot 2025-03-09 142945.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309144903.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309144928.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309145032.png)

> [!Success] Answer
> Cross Site Scripting (Reflected)

# Task 5 - Authenticated Scans

- By default, ZAP won't be able to check any parts that require authentication without the provided credentials
- We can record the authentication process through scripts
	- Can then test those scripts to see if it was recorded properly
- **Context**
	- Tells ZAP where to use our scripts within a group of URLs
	- Can make it go through all possible URLs on target since it's small and simple
	- Can configure a variety of options under a context, like for authentication purposes to use our newly defined script
- Can then re-spider the application under our new context
- **Preventing log outs**
	- Can provide sites to be excluded from the context like a logout page that logs out our spider session.
	- Also can go within each response to exclude any logout links on each response
	- Can provide the context **Authentication logged-out indicators** like text that mentions about logging in


> [!Question]
>  **Which type of script was used to record the authentication process to our site in ZAP?**

> [!Success] Answer
> ZEST scripts

> [!Question]
>  **What additional high-risk vulnerability was found on the site after running the authenticated scan?**

First had to record a Zest script for our authentication login process

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309151417.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309151615.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309151626.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309151646.png)

Credentials given to us in the room as, **nospiders**, for both username and password

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309151730.png)

Once done, clicked the same button on toolbar in ZAP to stop recording the script.

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309151935.png)

Can run the script again to ensure that it was recorded correctly

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309152128.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309152139.png)

Can also check the response to see where it redirects you, in this case, it went to `./cowsay.php`

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309152227.png)

Can now create a context around this website for us to run our new scripts

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309152324.png)

Can load our Zest script as our authentication method for this context

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309152418.png)

Do need to create a user for this context in order for our authentication process to run.

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309152548.png)

Any sites now apart of the context has a new target icon to it indicating them being apart of the group

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309152617.png)

Can re run our spider script with the new context and script along with our new user

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309152801.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309152859.png)

Once ran, we can see the newly added nodes that were previously inaccessible through authentication measures

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309153003.png)

Can now focus on trying to prevent our spider from logging out.

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309153059.png)

Check though nodes that are behind the authentication to check for any indicators of whether the spider is logged in or not

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309153335.png)

Can also check for login authenticators.

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309154003.png)

Can also create verification strategy that tells the spider how to check for whether it's logged in or not. In this case, we can tell it to check a specific URL (aboutme.php) to check for the patterns within the HTML to see if it's logged in or out.

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309154151.png)

Can run another scan with the created context and user to find any new vulnerabilities

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309154714.png)

> [!Success] Answer
> Remote OS Command Injection

# Task 6 - Checking APIs with ZAP

- Not easy to spider APIs since their endpoints are usually not exposed nor does it tell information about other endpoints
	- Also need parameters required in order to get responses
- Can get a export from the development team about each of the API endpoints with the required parameters
	- Can load export into ZAP to then scan

> [!Question]
>  **What high-risk vulnerability was found on the `/asciiart/generate` endpoint?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309160345.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309160421.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309160443.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309160520.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309160531.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309160817.png)

> [!Success] Answer
> Remote OS Command Injection

> [!Question]
>  **Read the details on the Path Traversal vulnerability detected. Based solely on the information presented by the scanner, would you categorise this finding as a false positive? (yea/nay)?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309160849.png)

Would classify this as a false positive due to APIs being constraint in only allowing set information to come out. Does not allow for any methods of path traversal within the endpoint.

> [!Success] Answer
> Yea

# Task 7 - Integrating DAST Into the Development Pipeline 

- Before integrating need to answer some questions like
	- Which stage to run the scan
	- What will trigger the scan
	- Determine intensity of each scan
- Provides early visibility of vulnerabilities. 
	- Run automatically on each commit and will test for a subset of vulnerabilities 
	- Avoids long delays in the pipeline.

> [!Question]
>  **Download the ZAP report for the simple-webapp repository. How many medium-risk vulnerabilities were found?**

First logged into gitea using the given credentials, **thm**, for both username and password in order to set up the stage to run the ZAP scan within the **Jenkinsfile**.

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309162045.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309162221.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309162242.png)

Uncommented the last part in order to set the stage to scan with the OWASP ZAP.

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309162304.png)

Can login into Jenkins using the provided credentials, **thm**, for both username and password

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309161735.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309162509.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309162854.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309163057.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309163024.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309163119.png)

> [!Success] Answer
> 3

> [!Question]
>  **Check the main branch of the simple-api repository on Jenkins. One of the builds failed during the Build the Docker image step. What is the number of the pre-existing failed build?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250309163157.png)

> [!Success] Answer
> 4

> [!Question]
>  **Download the ZAP report for the `simple-api` repository. What high-risk vulnerability was found?**

Repeated the same steps as earlier to produce the report, this time for the `simple-api` repository.

![](/img/user/TryHackMe/THM_Images/1_h-elqXEJpe6G0UhxxDUBmw.webp)

> [!Success] Answer
> Remote OS Command Injection
