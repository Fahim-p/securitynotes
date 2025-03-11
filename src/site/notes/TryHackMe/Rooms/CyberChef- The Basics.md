---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/cyber-chef-the-basics/","created":"2024-11-25T16:50:00.000-05:00","updated":"2025-03-11T00:32:59.092-04:00"}
---

# Task 3 - Navigating the Interface

- 4 Areas
	- **Operations**
		- Repository of all operations that CyberChef can preform
	- **Recipe**
		- Can select, arrange, and fine-tune operations to suit needs
		- Define operation arguments and options
		- BAKE!
			- Processes the data with the given recipe
			- Can automate this process with the “Auto Bake” checkbox
	- **Input**
		- Allows for input of text or files to perform operations
		- Can input folders or files as inputs
	- **Output**
		- Showcases data processing results, presents outcomes of manipulations/transformations to input data

![1000](/img/user/TryHackMe/THM_Images/06a10182648aa4f0ab9aadb68bf00f2b.png)

> [!Question]
> 
> **In which area can you find "From Base64"?**

> [!Success] Answer
Operations

> [!Question]
> 
> **Which area is considered the heart of the tool?**

> [!Success] Answer
Recipe

# Task 5 - Practice, Practice, Practice

- Extractors

| Specific                         | Description                           |
| -------------------------------- | ------------------------------------- |
| Extract IP addresses             | Extracts all IPv4 and IPv6 addresses. |
| Extract URLs                     | Extracts URLs from the input.         |
| Protocol (HTTP, FTP) is required |                                       |
| Extract email addresses          | Extracts all email addresses          |

- Date and Time 

|Specific|Description|
|---|---|
|From UNIX Timestamp|Converts a UNIX timestamp to a datetime string.|
|To UNIX Timestamp|Parses a datetime string in UTC and returns the corresponding UNIX timestamp.|

- Unix timestamp is a 32-bit value representing the number of seconds since January 1, 1970 UTC
- Data Format

| Operations  | Description                                                                                                                                                                                                                             | Examples                                                                                      |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| From Base64 | Decodes data from an ASCII Base64 string back into its raw format.                                                                                                                                                                      | `V2VsY29tZSB0byB0cnloYWNrbWUh` becomes `Welcome to tryhackme!`                                |
| URL Decode  | Converts URI/URL percent-encoded characters back to their raw values.                                                                                                                                                                   | `https%3A%2F%2Fgchq%2Egithub%2Eio%2FCyberChef%2F` becomes `https://gchq.github.io/CyberChef/` |
| From Base85 | Notation for encoding arbitrary byte data.  <br>This operation decodes data from an ASCII string (with an alphabet of your choosing, presets included).                                                                                 | `BOu!rD]j7BEbo7` becomes `hello world`                                                        |
| From Base58 | Notation for encoding arbitrary byte data.  <br>Differs from Base64 by removing efficiently misread characters (i.e. l, I, 0, and O) to improve human readability.                                                                      | `AXLU7qR` becomes`Thm58`                                                                      |
| To Base62   | Notation for encoding arbitrary byte data using a restricted set of symbols that humans can conveniently use and process by computers.  <br>The high number base results in shorter strings than with the decimal or hexadecimal system | `Thm62` becomes`6NiRkOY`                                                                      |

> [!Question]
> **What is the hidden email address?**

Inputted given file into the Input field, went to Operations and dragged the “Extract email address” operation into the Recipe, baked it to get the answer, hidden@hotmail.com

![1000](/img/user/TryHackMe/THM_Images/887d39d077526e7282cca1ba8dfa8694.png)

> [!Success] Answer
> hidden@hotmail.com

> [!Question]
> **What is the hidden IP address that ends in .232?**

Inputted given file into the Input field, went to Operations and dragged the “Extract IP addresses” operation into the Recipe, baked it to get two IP addresses.

![1000](/img/user/TryHackMe/THM_Images/859492c8e6852ed233b013ca72e34363.png)

> [!Success] Answer 
102.20.11.232

> [!Question]
> 
> **Which domain address starts with the letter "T"?**

Inputted given file into the Input field, went to Operations and dragged the “Extract domains” operation into the Recipe, baked it to get two IP domains.

![1000](/img/user/TryHackMe/THM_Images/8123856540ca20c08a7e8e9152b0022e.png)

> [!Success] Answer
TryHackMe.com

> [!Question]
> 
> **What is the binary value of the decimal number 78?**

Inputted 78 into the input field, went to Data Format and dragged first the “From Decimal” operation into the Recipe and then “To Binary”, baked it to get the answer, 01001110.

![1000](/img/user/TryHackMe/THM_Images/2827a967ef8d76421b765b3b4c6de83d.png)

> [!Success] Answer
01001110

> [!Question]
> 
> **What is the URL encoded value of `https://tryhackme.com/r/careers`**

Inputted "[https://tryhackme.com/r/careers](https://tryhackme.com/r/careers)” into the input field, went to Networking and dragged “URL Encode” operation into the Recipe , baked it to get the answer, [https://tryhackme.com/r/careers](https://tryhackme.com/r/careers).

![1000](/img/user/TryHackMe/THM_Images/342b6d82cf197461528e626b44d3fa26.png)

> [!Success] Answer
[https://tryhackme.com/r/careers](https://tryhackme.com/r/careers)

# Task 6 - Your First Official Cook

> [!Question]
> **Using the file you downloaded in Task 5, which IP starts and ends with "10"?**

![1000](/img/user/TryHackMe/THM_Images/662c27b70197758700011b87efcfedee.png)

> [!Success] Answer
10.10.2.10

> [!Question]
> **What is the base64 encoded value of the string "Nice Room!"?**

![1000](/img/user/TryHackMe/THM_Images/234b4297bf9971a995b079141889f2fe.png)

> [!Success] Answer
TmljZSBSb29tIQ==

> [!Question]
> 
>**What is the URL decoded value for `https%3A%2F%2Ftryhackme%2Ecom%2Fr%2Froom%2Fcyberchefbasics`**

![1000](/img/user/TryHackMe/THM_Images/b78ba6e097308ebfe4ebc6990813962c.png)

> [!Success] Answer 
[https://tryhackme.com/r/room/cyberchefbasics](https://tryhackme.com/r/room/cyberchefbasics)

> [!Question]
> 
> **What is the datetime string for the Unix timestamp `1725151258`?**

![1000](/img/user/TryHackMe/THM_Images/9a33811908cd8eff1e2c175bc81e01f2.png)

> [!Success] Answer
Sun 1 September 2024 00:40:58 UTC

> [!Question]
> 
> **What is the Base85 decoded string of the value `<+oue+DGm>Ap%u7`?**

![1000](/img/user/TryHackMe/THM_Images/3c72877973ec29a0ac74b278842d7889.png)

> [!Success] Answer
This is fun!