---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/owasp-api-security-top-10/","created":"2025-02-22T17:39:21.478-05:00","updated":"2025-03-11T00:32:59.343-04:00"}
---

# Vulnerability 1: Broken Object Level Authorization (BLOA)

- **How does it Happen?**
	- API endpoints are utilized for a common practice of retrieving and manipulating data through object identifiers. 
	- Scenario where the user uses the **input functionality and gets access to the resources they are not authorized to access**. 
		- Usually implemented through programming in Models (Model-View-Controller Architecture) at the code level.
- **Likely Impact**
	-  Data leakage, complete account takeover. 
- **Practical Example**  
	- Bob is working as an API developer in `Company MHT` 
		- Developed an endpoint `/apirule1/users/{ID}` 
			- Allows other applications or developers to request information by sending an employee ID. 
			- Can send `GET` requests to `http://localhost:80/MHT/apirule1_v/user/1.`
	- Major issue is that **endpoint is not validating any incoming API call** to confirm whether the request is valid.
		- Not checking for any authorization whether the person requesting the API call can ask for it or not.  
	- Bob can implement an authorization mechanism through which he can identify who can make API calls to access employee ID information.  
		- Achieved through **access tokens or authorization tokens** in the header. 
			- Bob can add an authorization token so that only headers with valid authorization tokens can make a call to this endpoint.
			- Can add valid `Authorization-Token` header to the request
				- Only then he'll get the correct results from the call `http://localhost:80/MHT/apirule1_s/user/1`
			- All API calls with an invalid token will show `403 Forbidden` an error message
- **Mitigation Measures**
	- An authorization mechanism that relies on user policies and hierarchies should be adequately implemented. 
	- Check if the logged-in user is authorized to perform specific actions. 
	- Promote using completely random values (strong encryption and decryption mechanism) for nearly impossible-to-predict tokens.

> [!Question]
>  **Suppose the employee ID is an integer with incrementing value. Can you check through the vulnerable API endpoint the total number of employees in the company?**

Tried all incrementing values starting from 1 until I don't get a valid response. 3 was the last number in which I had a valid response of 200 

![](/img/user/TryHackMe/THM_Images/8d46bb176c3804161474dc9130a5bbfa.png)

> [!Success] Answer
> 3

> [!Question]
>  **What is the flag associated with employee ID 2?**

![](/img/user/TryHackMe/THM_Images/2f30e6fb4541fbde262add85d22e7db9.png)

> [!Success] Answer
> THM{838123}

> [!Question]
>  **What is the username of employee ID 3?**

![](/img/user/TryHackMe/THM_Images/c1874016e3549f391087e1bd940ad607.png)

> [!Success] Answer
> Bob
# Vulnerability 2: Broken User Authentication (BUA)

- **How does it happen?**
	- Scenario where an API endpoint allows an attacker to access a database or acquire a higher privilege than the existing one. 
	- **Invalid implementation of authentication** like using incorrect email/password queries
		- Absence of security mechanisms like authorization headers, tokens etc.
- **Likely Impact** 
	- Can compromise the authenticated session or the authentication mechanism and easily access sensitive data. 
	- Impersonation of an authorized individual and can conduct an undesired activity, including a complete account takeover. 
- **Practical Example**  
	- Bob understands that authentication is critical and has been tasked to develop an API endpoint `apirule2/user/login_v` that will authenticate based on provided email and password.
		- Will return a token, which will be passed as an `Authorization-Token` header (GET request) to `apirule2/user/details` to show details of the specific employee. 
		- Only used email to validate the user from the `user table` and ignored the password field in the SQL query. 
			- Attacker only requires victim's email address to get a valid token or account takeover.
	-  Can test this by sending a `POST` request to `http://localhost:80/MHT/apirule2/user/login_v` with email and password in the form parameters.
		- Vulnerable endpoint received a token which can be forwarded to `/apirule2/user/details` to get detail of a user.
	- Need to update the login query logic and use both email and password for validation. 
		- `/apirule2/user/login_s` is a valid endpoint, authorizes the user based on password and email both.
- **Mitigation Measures** 
	- Ensure complex passwords with higher entropy for end users.
	- Do not expose sensitive credentials in **GET** or **POST** requests.
	- Enable strong JSON Web Tokens (JWT), authorization headers etc.
	- Ensure the implementation of multifactor authentication (where possible), account lockout, or a captcha system to mitigate brute force against particular users. 
	- Ensure that passwords are not saved in plain text in the database to avoid further account takeover by the attacker.


> [!Question]
>  **Can you find the token of hr@mht.com?**

![](/img/user/TryHackMe/THM_Images/a8e6d1245d4e949bd5a18b290aa41b75.png)

> [!Success] Answer
> cOC%Aonyis%H)mZ&uJkuI?_W#4&m>Y

> [!Question]
>  **To which country does sales@mht.com belong?**

![](/img/user/TryHackMe/THM_Images/a40143fb8a433aa17ec9a743f3426fdc.png)

Authentication token for sales@mht.com: ~jSkQD:u<Zdo!JDvX_9V[GrD%:JTtU

![](/img/user/TryHackMe/THM_Images/da6dece73b7cf7ffcc354ee016fc624f.png)

> [!Success] Answer
> China

> [!Question]
>  **Is it a good practice to send a username and password in a GET request (yea/nay)?**

> [!Success] Answer
> nay

# Vulnerability 3: Excessive Data Exposure

- **How does it happen?**
	- Excessive data exposure occurs when applications tend to **disclose more than desired information** to the user through an API response. 
		- Tend to expose all object properties without considering their sensitivity level. 
		- Filtration task is to the front-end developer before it is displayed to the user. 
	- Can intercept the response through the API and quickly extract the desired confidential data.
	- The runtime detection tools or the general security scanning tools can give an alert on this kind of vulnerability
		- Cannot differentiate between legitimate data that is supposed to be returned or sensitive data. 
- **Likely Impact** 
	- Can sniff traffic and easily access confidential data, including personal details
	- APIs respond with sensitive tokens that can be later on used to make calls to other critical endpoints.
- **Practical Example**  
	- Bob develops an endpoint `apirule3/comment_v/{id}` that fetches all information available for a comment from the database. 
		- Assumption that the front-end developer would filter out information while showing it on the company's main website.
		- He configures it so the API is sending more data than desired. 
			- Instead of relying on a front-end engineer to filter out data, only relevant data must be sent from the database.
	- Bob then updates the endpoint and created a valid endpoint `/apirule3/comment_s/{id}` that returns only the necessary information to the developer
- **Mitigation Measures** 
	- Never leave sensitive data filtration tasks to the front-end developer. 
	- Ensure time-to-time review of the response from the API to guarantee it returns only legitimate data and checks if it poses any security issue. 
	- Avoid using generic methods such as `to_string() and to_json()`. 
	- Use API endpoint testing through various test cases and verify through automated and manual tests if the API leaks additional data.

> [!Question]
>  **What is the device ID value for post-ID 2?**

![](/img/user/TryHackMe/THM_Images/1b4d27b8b121dea26515b95c802db03d.png)

> [!Success] Answer
> iOS15.411

> [!Question]
>  **What is the username value for post-ID 3?**

![](/img/user/TryHackMe/THM_Images/84d80aa5c3430e72cb3be0dea38fa6bb.png)

> [!Success] Answer
> hacker#!

> [!Question]
>  **Should we use network-level devices for controlling excessive data exposure instead of managing it through APIs (programmatically) - (yea/nay)?**

> [!Success] Answer
> nay

# Vulnerability 4: Lack of Resources & Rate Limiting

- **How does it happen?**
	- Lack of resources and rate limiting means that **APIs do not enforce any restriction on** the frequency of clients' requested resources or the files' size
		- Affects the API server performance and leads to the DoS or non-availability of service. 
		- Consider a scenario where an API limit is not enforced, 
			- Allows a user to upload several GB files simultaneously or make any number of requests per second. 
			- Excessive resource utilization in network, storage, compute etc.
	- Nowadays, attackers are using such attacks to ruin brand reputation through increased downtime.
		- A simple example is non-compliance with the Captcha system on the login form
		- Allows anyone to make numerous queries to the database through a small script written in Python.
- **Likely Impact** 
	- The attack primarily targets the **Availability** principles of security
	- Can tarnish the brand's reputation and cause financial loss.  
- **Practical Example**
	- Bob successfully develops a login API, but there must be a "Forgot Password" option that can be used to recover an account.  
	- He started building an endpoint `/apirule4/sendOTP_v` that will send a 4-digit numeric code to the user's email address. 
		- OTP is used by user to recover account.
	- Malicious actor can write a small script and brute force the endpoint, sending many emails in a few seconds
	- Bob comes up with an intelligent solution `(/apirule4/sendOTP_s)` 
		- Enabled rate limiting such that the user has to wait 2 minutes to request an OTP token again.
- **Mitigation Measures** 
	- Ensure using a captcha to avoid requests from automated scripts and bots.
	- Ensure implementation of a limit, i.e., how often a client can call an API within a specified time and notify instantly when the limit is exceeded. 
	- Ensure to define the maximum data size on all parameters and payloads, i.e., max string length and max number of array elements.

> [!Question]
>  **Can rate limiting be carried out at the network level through firewall etc. (yea/nay)?**

> [!Success] Answer
> yea

> [!Question]
>  **What is the HTTP response code when you send a POST request to /apirule4/sendOTP_s using the email address hr@mht.com?**

![](/img/user/TryHackMe/THM_Images/8b7e840301b1c7901c5c97bce6b5623e.png)

> [!Success] Answer
> 200

> [!Question]
>  **What is the "msg key" value after an HTTP POST request to /apirule4/sendOTP_s using the email address sale@mht.com?**

![](/img/user/TryHackMe/THM_Images/f93a397fe0f71355671461ad63e38e2d.png)

> [!Success] Answer
> nay

# Vulnerability 5: Broken Function Level Authorization

- **How does it happen?**
	- Scenario where a low privileged user bypasses system checks and gets access to **confidential data by impersonating a high privileged user**. 
		- Complex access control policies with hierarchies, roles, and groups and a vague separation between regular and administrative functions can lead to severe authorization flaws. 
			- Intruders can easily access the unauthorized resources of another user or administrative functions.   
	- Reflects IDOR permission, where a user can perform administrative-level tasks. 
		- More prone to APIs with complex user roles/permissions. 
- **Likely Impact** 
	- The attack primarily targets the authorization and non-repudiation principles of security
	- Impersonation of an authorized user and let the malicious actor get administrative rights to perform sensitive tasks. 
- **Practical Example**  
	- Bob developed an endpoint `/apirule5/users_v` to fetch data of all employees from the database. 
		- To add protection, he added another layer to security by adding a special header `isAdmin` in each request. 
		- Only fetches employee information from the database if `isAdmin=1` and `Authorization-Token` are correct. 
	-  A non-admin user can access the endpoint with customized requests to it with `isAdmin value = 1`. 
		- The authorization token for HR user Alice is `YWxpY2U6dGVzdCFAISM6Nzg5Nzg=`, can be used alongside the `isAdmin` value to send requests
	- Can be resolved by implementing correct authorization rules and checking the functional roles of each user in the database during the query.
		- Bob implemented another endpoint `/apirule5/users_s` that validates each user's role and only shows employees' data if the role is Admin.
- **Mitigation Measures** 
	- Ensure proper design and testing of all authorisation systems and deny all access by default. 
	- Ensure that the operations are only allowed to the users belonging to the authorised group. 
	- Make sure to review API endpoints against flaws regarding functional level authorisation and keep in mind the apps and group hierarchy's business logic.

> [!Question]
>  **What is the mobile number for the username Alice?**

Used alice's authorization token to bypass the check.

![](/img/user/TryHackMe/THM_Images/72f7b897dcbfa2dc452240b063a58fab.png)

> [!Success] Answer
> +1235322323

> [!Question]
>  **Is it a good practice to send isAdmin value through the hidden fields in form requests - yea/nay?**

> [!Success] Answer
> nay

> [!Question]
>  **What is the address flag of username admin?**

Refer to previous screenshot

> [!Success] Answer
> THM{3432$@#2!}

# Vulnerability 6 - Mass Assignment

- **How does it happen?**
	- Scenario where **client-side data is automatically bound with server-side objects or class variables**. 
		- Feature is exploited through understanding the **application's business logic** and sending specially crafted data to the server
		- Acquires administrative access or inserting tampered data.
	- Consider a username of the user is a read-only attribute and cannot be changed
		- A malicious actor can edit the username and submit the form. 
			- If necessary filtration is not enabled on the server side (model), it will simply insert/update the data in the database. 
- **Likely Impact** 
	- **Data tampering and privilege escalation** from a regular user to an administrator. 
- **Practical Example**  
	- Bob has been assigned to develop a signup API endpoint `/apirule6/user` that will take in input parameters (POST). 
		- The user's table has a `credit column` with a default value of `50`
		- Users will upgrade their membership to have a larger credit value.
	- Bob uses mass assignment feature in Laravel to store all the incoming data from the client side to the database 
	- No filtering on the server side. 
		- Since using the **mass assignment feature**, he is also inserting credit values in the database 
		- Malicious actors can update that value  
	- Need to ensure necessary filtering on the server side (`apirule6/user_s`) and ensure that the default value of credit should be inserted as `50`, even if more than 50 is received from the client side
- **Mitigation Measures** 
	- Before using any framework, one must study how the backend insertions and updates are carried out. In the Laravel framework, [fillable and guarded](https://laravel.com/docs/9.x/eloquent#inserts) arrays mitigate the above-mentioned scenarios. 
	- Avoid using functions that bind an input from a client to code variables automatically.
	- Allowlist those properties only that need to get updated from the client side.

> [!Question]
>  **Is it a good practice to blindly insert/update user-provided data in the database (yea/nay)?**

> [!Success] Answer
> nay

> [!Task]
>  **Using /apirule6/user_s, insert a record in the database using the credit value as 1000**

![](/img/user/TryHackMe/THM_Images/f4ea8c613ea8486a2c3cc02fc2fe6ce7.png)

> [!Question]
>  **What would be the returned credit value after performing Question#2?**

Refer to previous screenshot

> [!Success] Answer
> 50
# Vulnerability 7 - Security Misconfiguration

- **How does it happen?**
	- **Incorrect and poorly configured security controls** that put the security of the whole API at risk. 
	- Several factors can result in security misconfiguration
		- Improper/incomplete default configuration, 
		- Publicly accessible cloud storage,
		- [Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS), 
		- Error messages displayed with sensitive data. 
	- Can take advantage of these misconfigurations to perform detailed reconnaissance and get unauthorized access to the system. 
	- Usually detected by vulnerability scanners or auditing tools and thus can be stopped at the initial level. 
		- API documentation, a list of endpoints, error logs etc., **must not be publicly accessible** to ensure safety against security misconfigurations.
		- Companies deploy security controls like web application firewalls, which are not configured to block undesired requests and attacks.  
	- **Likely Impact** 
		- Can give intruders complete knowledge of API components. 
			- Allows intruders to bypass security mechanisms. 
			- **Stack trace or other detailed errors** can provide the malicious actor access to confidential data and essential system details  
- **Practical Example**  
	- Bob develops an API endpoint `/apirule7/ping_v` (GET) that will share details regarding server health and status.
	- Bob forgets to implement any error handling to avoid any information leakage.
	- In case of an unsuccessful call, the server sends a complete stack trace in response, 
		- Containing function names, controller and route information, file path etc.
		- Attacker can use the information for profiling and preparing specific attacks on the environment.  
	- Bob then creates a API endpoint `/apirule7/ping_s` that will carry out error handling and only share desired information with the user
- **Mitigation Measures** 
	- Limit access to the administrative interfaces for authorized users and disable them for other users. 
	- Disable default usernames and passwords for public-facing devices (routers, Web Application Firewall etc.).
	- Disable directory listing and set proper permissions for every file and folder. 
	- Remove unnecessary pieces of code snippets, error logs etc. and turn off debugging while the code is in production.


> [!Question]
>  **Is it an excellent approach to show error logs from the stack trace to general visitors (yea/nay)?**

> [!Success] Answer
> nay

> [!Task]
>  **Try to use the API call /apirule7/ping_s in the attached VM**

![](/img/user/TryHackMe/THM_Images/0824e50bda9fffcb53b0939a6b06faa4.png)

> [!Question]
>  **What is the HTTP response code?**

Refer to previous screenshot

> [!Success] Answer
> 500

> [!Question]
>  **What is the Error ID number in the HTTP response message?**

Refer to previous screenshot

> [!Success] Answer
> 1401
# Vulnerability 8 - Injection

- **How does it happen?**
	- Occurs when user input is **not filtered and is directly processed by an API**
		- Enabling the attacker to perform unintended API actions without authorization.  
	- May come from SQL, OS commands, XML, etc 
	- Many recent frameworks offer functionality to protect against this attack through automatic sanitization of data
		- Applications built in custom frameworks like core PHP are still susceptible to such attacks 
- **Likely Impact** 
	- **Information disclosure, data loss, DoS, and complete account takeover**
	- Access the sensitive data or even create new functionality and perform remote code execution 
- **Practical Example**  
	- Bob developed a vulnerable login API endpoint `/apirule8/user/login_v` that is not filtering user input.  
		- A malicious attacker requires the username of the target, and for the password, they can use the payload `' OR 1=1--'` and get an authorization key for any account
	- Bob updates the API endpoint to `/apirule8/user/login_s` and used parameterized queries and built-in filters of Laravel to sanitize user input.
		- Malicious payloads on username and password parameters were effectively mitigated
- **Mitigation Measures**
	- Ensure to use a well-known library for client-side input validation.
	- If a framework is not used, all client-provided data must be validated first and then filtered and sanitized. 
	- Add necessary security rules to the Web Application Firewall (WAF). 
		- Injection flaws can be mitigated at the network level.
	- Make use of built-in filters in frameworks like Laravel, Code Ignitor etc., to validate and filter data.

> [!Question]
>  **Can injection attacks be carried out to extract data from the database (yea/nay)?**

> [!Success] Answer
> yea

> [!Question]
>  **Can injection attacks result in remote code execution (yea/nay)?**

> [!Success] Answer
> yea

> [!Question]
>  **What is the HTTP response code if a user enters an invalid username or password?**

![](/img/user/TryHackMe/THM_Images/cf45bffc7679770d279494e58e98fca6.png)

> [!Success] Answer
> 403

# Vulnerability 9: Improper Assets Management

- **How does it happen?**
	- Scenario where we have **two versions of an API available in our system**
		- Let's name them APIv1 and APIv2
			- Everything is wholly switched to APIv2, but the previous version, APIv1, has not been deleted yet. 
			- Possible that APIv1 doesn't have the updated or the latest security features. 
	- Not properly tracking API endpoints. 
		- Incomplete API documentation or absence of compliance with the [Software Development Life Cycle](https://tryhackme.com/room/securesdlc). 
	- A properly maintained, up-to-date API inventory and proper documentation are more critical than hardware-based security control for an organization.  
- **Likely Impact** 
	- Unauthorized access to confidential data or even complete control of the system. 
- **Practical Example**  
	- MHT has developed different API versions like v1 and v2. 
		- Forgot to remove the old version from the server.  
	- Found that old API calls like `apirule9/v1/user/login` return more information like balance, address etc., against the user
	- Bob had to deactivate old and unused assets so that users can only access limited and desired information from the new endpoint `/apirul9/v2/user/login`
- **Mitigation Measures**   
	- Access to previously developed sensitive and deprecated API calls must be blocked at the network level.
	- APIs developed for R&D, QA, production etc., must be segregated and hosted on separate servers.
	- Ensure documentation of all API aspects, including authentication, redirects, errors, CORS policy, and rate limiting. 
	- Adopt open standards to generate documentation automatically.

> [!Question]
>  **Is it good practice to host all APIs on the same server (yea/nay)?**

> [!Success] Answer
> nay

> [!Task]
>  **Make an API call to /apirule9/v1/user/login using the username "Alice" and password "##!@#!!".**

![](/img/user/TryHackMe/THM_Images/6a69febf30c4aff0a4501dbbbe9b8d77.png)

> [!Question]
>  **What is the amount of balance associated with user Alice?**

Refer to previous screenshot

> [!Success] Answer
> 100

> [!Question]
>  **What is the country of the user Alice?**

Refer to previous screenshot

> [!Success] Answer
> USA

# Vulnerability 10 - Insufficient Logging & Monitoring

- **How does it happen?**
	- Scenario when an attacker conducts malicious activity on your server; 
	- **Not enough evidence available to track attacker due to the absence of logging and monitoring mechanisms**. 
	- Many companies lack API logging and monitoring. 
		- Visitor's IP address, endpoints accessed, input data, timestamp, etc. 
	- Enables the identification of threat attack patterns.
	- Latest web frameworks can automatically log requests at different levels like error, debug, info etc. 
		- Logged in a database or file or even passed to a [SIEM solution](https://tryhackme.com/room/defensivesecurity) for detailed analysis.
- **Likely Impact** 
	- Inability to identify attacker or hacker behind the attack. 
- **Practical Example**  
	- Bob makes an API endpoint `/apirule10/logging` (GET) that will log users' metadata (IP address, browser version etc.) and save it in the database as well
		- Forwarded to a SIEM solution for correlation and analysis.
- **Mitigation Measures** 
	- Ensure use of SIEM for log management. 
	- Keep track of all denied accesses, failed authentication attempts, and input validation errors, using a format imported by SIEM and enough detail to identify the intruder.
	- Handle logs as sensitive data and ensure their integrity at rest and transit. Moreover, implement custom alerts to detect suspicious activities as well.

> [!Question]
>  **Should the API logs be publically accessible so that the attacker must know they are being logged (yea/nay)?**

> [!Success] Answer
> nay

> [!Question]
>  **What is the HTTP response code in case of successful logging of user information?**

![](/img/user/TryHackMe/THM_Images/4bfe89e8fb6da623537ff15f30e03317.png)

> [!Success] Answer
> 200
