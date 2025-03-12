---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/sast/","created":"2025-02-24T17:37:54.724-05:00","updated":"2025-03-12T00:21:28.606-04:00"}
---

# Task 2 - Code Review

Information already known in  [SSDLC](SSDLC.md)


> [!Question]
>  **Are automated code reviews a substitute for manual reviewing? (yea/nay)?**

> [!Success] Answer
> nay

> [!Question]
>  **What type of code review will run faster? (Manual/Automated)**

> [!Success] Answer
> Automated

> [!Question]
>  **What type of code review will be more thorough? (Manual/Automated)**

> [!Success] Answer
> Manual
# Task 3 - Manual Code Review

- Goal to find SQL injection vulnerabilities in source code of simple application
- **Searching for Insecure Functions**
	- First step, should focus on any functions that could be used to send raw queries to the database.
	- **Check functions that are used to send MySQL queries**
		- mysqli_query(), mysql_query(), mysqli_prepare(), query(), prepare()
	- Can manually search instances of such functions in all of our project's files recursively. 
		- Can use `grep` to find instances of functions being used
		- `grep -r -n 'mysqli_query('`
			- `-r`, recursive search for all files under current directory
			- `-n`, show line number where it occurred
		- If there are instances shown, then can go within file where found and look more closely
![](/img/user/TryHackMe/THM_Images/1ca950bc88a8d21f8a6c92025b8165dd.png)
```
## html/db.php

function db_query($conn, $query){
    $result = mysqli_query($conn, $query);
    return $result;
}
```

- Common for functions to be nested into other functions
- **Analyzing local context of a function is not enough to determine if a vulnerability is present.** 
	- Need to trace the uses of the `db_query()` function throughout the code to identify potential vulnerabilities.
	- Can do so once again with `grep`
		- `grep -r -n 'db_query('`
![](/img/user/TryHackMe/THM_Images/df7b34547d4e301aade07eb5331374c0.png)

Need to investigate these results within the corresponding file

First instance
![](/img/user/TryHackMe/THM_Images/ece2d029a95872f6fec5f4fd28db5023.png)
- Code above is a instance of an SQL injection
	- `guest_id` parameter is concatenated into raw SQL query without input sanitization
	- **Code is vulnerable**

Second instance
![](/img/user/TryHackMe/THM_Images/66f43534becfb211a6245b32ddc4bf71.png)
- GET parameters being concatenated into SQL queries. 
	- Are sanitized through `preg_replace()` using different regular expressions to replace any character that isn't allowed with an empty string.
	- Need to evaluate if filters in place present vulnerabilities.
		- Only allows characters that are either alphanumeric or double-quotes.
		- SQL sentence encloses the string passed through `$_GET['log_id']` between single-quotes ('). 
		- No way for attacker to escape from the string in the SQL sentence
			- Code **isn't vulnerable**
Third instance
![](/img/user/TryHackMe/THM_Images/a69840dae6dacaad7f7a84a77ab5b967.png)
- Allows only numeric characters to be passed through `$_GET['art_id']`. 
	- `preg_replace()` function is called with a third parameter set to "1". 
		- Indicates the maximum number of replacements to be done. 
		- Since it is set to 1, only the first character that isn't a number will be replaced with an empty string. 
			- Any other characters will pass without being replaced, enabling SQL injections. 
				- Code **is vulnerable.**

> [!Task]
>  Local File Inclusion (LFI) attacks are made possible by the misuse of one of the following functions in PHP:
>  
>  require()	include()	require_once()	include_once()
>
>  **Answer the following questions using grep to search for LFI vulnerabilities only on the .php files in the html/ directory of the simple-webapp project**

Used the following command, `grep -r -n 'include(' --include=\*.php`

![](/img/user/TryHackMe/THM_Images/23cac4037d976b532bd03d4a2b706b9d.png)

Tried to search for any instances of the other functions being called, didn't find any.

![](/img/user/TryHackMe/THM_Images/8f88104b0f769765c2bd9d48b329658e.png)

> [!Question]
>  **How many instances of the function found in question 2 exist in your project's code?**

Used the command `grep -r -n -o 'include(' --include=\*.php | wc -l`

![](/img/user/TryHackMe/THM_Images/d39741a58d5cdc22f969e5f208e90f90.png)

> [!Success] Answer
> 9

> [!Question]
>  **Only one of the function's instances is vulnerable to LFI. Remember that for LFI to be present, the attacker must be able to manipulate a part of what is sent to the vulnerable function. The vulnerable instance must contain some reference to a GET or POST parameter or other manipulable inputs. 
>  What file contains the vulnerable instance?**

Only instance of file that includes a reference to a GET or POST parameter. All the other ones are used other php files

![](/img/user/TryHackMe/THM_Images/3917de964f62aa81fbde7bc27cdc949f.png)

> [!Success] Answer
> View.php

> [!Question]
>  **What line in the file found on the previous question is vulnerable to LFI?**

Refer to previous screenshot

> [!Success] Answer
> 22

# Task 4 - Automated Code Review 

- **Static Application Security Testing (SAST)** 
	- Refers to using automated tools for code analysis. 
	- Not to replace manual code reviews but to provide a simple method to automate simple code checks to quickly find vulnerabilities
- SAST complements DAST or SCA 
	- Provides holistic approach to application security during the development lifecycle.

SAST Pros/Cons

| **Pros:**<br><br>- It doesn't require a running instance of the target application.      <br>- It provides great coverage of the application's functionality.<br>- It runs fast as opposed to other dynamic techniques.<br>- SAST tools report exactly where vulnerabilities are in the code.<br>- Easy to integrate into your CI/CD pipeline. | **Cons:**<br><br>- The source code of an application is not always available (third-party apps).<br>- Prone to false positives.<br>- Can't identify vulnerabilities that are dynamic in nature.<br>- SAST tools are mostly language-specific. They can only check languages they know. |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

- **SAST Under the Hood**
	1. **Transform the code into an abstract model:** 
		- Ingest source code and produce an abstract representation for further analysis. 
		- **Abstract Syntax Trees (AST)**
			- Way for SAST tool to represent code
			- Easier code analysis, independent of  programming language in use. 
			- Crucial for later analysis
				- Possible for AST to not translate programming language feature so it won't be analyzed for security issues
	2. **Analyze the abstract model for security issues:** 
		- Different analysis techniques will be used to search for potential vulnerabilities in the code model.

**Semantic analysis**
- Compared to grepping for potentially insecure functions while doing manual code reviews. 
	- Aims to find flaws concerning the use of potentially insecure code in a **localized context**.
- Examples
	- Searching for calls to `mysqli_query()` where GET or POST parameters are directly concatenated into the query string
```php
mysqli_query($db, "SELECT * from users where username=".$_GET['username'])
```

**Dataflow analysis** 
- Potentially dangerous functions are in use, not clear whether a vulnerability or not through analyzing the local context around the function call.
	- For example, a function defined as follows: 
		- Analyzing local context of the call to a dangerous function is not enough
			- **Trace how information flows from inputs the user can manipulate to potentially vulnerable functions** 
			- Data inputs will be referred to as **sources**, and potentially vulnerable functions will be referred to as **sinks**. 
				- If data flows from a source to a sink without sanitization, **it's a vulnerability**.  
		- Would have to find all of its usages and trace back to see if any tainted input (the source) is sent to it, 
			- Finally ending up as part of the query executed by `mysqli_query()` (the sink).

```php
function db_query($conn, $query){
    $result = mysqli_query($conn, $query);
    return $result;
}
```

**Control flow analysis**
- Analyses the **order of operations** in the code in search for 
	- Race conditions
	- Use of uninitialized variables
	- Resource leaks
	- As an example, look at the following piece of Java code:
		- If the `cmd` property isn't defined, 
			- Call to `System.getProperty()` will return NULL. 
			- Calling the trim method from a NULL variable will throw an exception on runtime.

```javascript
String cmd = System.getProperty("cmd");  
cmd = cmd.trim();
```

**Structural analysis** 
- Analyses **specific code structures** of each programming language. 
	- Following best practices when declaring classes
	- Evaluating code blocks that may never execute (dead code), 
	- Correctly using try/catch blocks
	- Issues related to using insecure cryptographic material (weak keys or IVs).
	- Example of code that would be detected by structural analysis
		- Implementation of RSA with a key size of 1024
			- Considered insufficient by today's standards.

```php
$options = array('private_key_bits' => 1024, 'private_key_type' => OPENSSL_KEYTYPE_RSA);  
$res = openssl_pkey_new($options);
```

**Configuration analysis** 
- Searches for **application configuration flaws** rather than the code itself. 
	- Example, applications running under Internet Information Services will have a configuration file called `web.config`, 
		- PHP will hold all of its configuration options in a file called `php.ini`
		- By checking configurations, the tool will identify possible improvements.
	- Example of two configuration directives in PHP that would raise an alert 
		- Facilitates some attack vectors for RFI, SSRF or other:

```php
allow_url_include = On
allow_url_fopen = On
```


> [!Question]
>  **Does SAST require a running instance of the application for analysis? (yea/nay)?**

> [!Success] Answer
> nay

> [!Question]
>  **What kind of analysis would likely flag dead code segments?**

> [!Success] Answer
> Structural analysis

> [!Question]
>  **What kind of analysis would likely detect flaws in configuration files?**

> [!Success] Answer
> Configuration analysis

> [!Question]
>  **What kind of analysis is similar to grepping the code in search of flaws?**

> [!Success] Answer
> Semantic analysis

# Task 5 - Rechecking our Application with SAST Tools

- Rechecking our Application with **Psalm (PHP Static Analysis Linting Machine)** 
	- Simple tool for analyzing PHP code.
	- Already in machine as `pslam.xml`

```
<?xml version="1.0"?>
<psalm
    errorLevel="3"
    resolveFromConfigFile="true"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns="https://getpsalm.org/schema/config"
    xsi:schemaLocation="https://getpsalm.org/schema/config vendor/vimeo/psalm/config.xsd"
    findUnusedBaselineEntry="true"
>
    <projectFiles>
        <directory name="html/" />
        <ignoreFiles>
            <directory name="vendor" />
        </ignoreFiles>
    </projectFiles>
</psalm>
```

- `errorLevel` 
	- How strict Psalm will be when reporting issues
	- The lower the value, the more issues will be reported 
- `projectFiles`  
	- Files to be scanned are indicated. 
	- Only the html directory will be scanned
		- Vendor directory will be ignored 
- Can run Psalm with the following **command**
	- `./vendor/bin/psalm --no-cache`
- Default only run some **structural analysis** over the code and show us programming errors that need our attention.
	- Search for issues with variable types, variable initialization and other safe coding patterns. 
	- **Not vulnerabilities**, but makes recommendations so your code follows coding best practices
- Can run **dataflow analysis** using the `--taint-analysis` flag. 
	- The output for this command will **pinpoint possible security issues.**

```shell-session
ERROR: TaintedInclude - html/view.php:22:9 - Detected tainted code passed to include or similar (see https://psalm.dev/251)
  $_GET
    <no known location>

  $_GET['img'] - html/view.php:22:28
include('./gallery-files/'.$_GET['img']);

  concat - html/view.php:22:9
include('./gallery-files/'.$_GET['img']);
```

- For each error reported, Shows a complete trace of the data flow from the source (`$_GET`) to the sink function (`include()`). 
	- This case is a LFI vulnerability
	- GET parameter `img` is concatenated directly into the filename passed to the `include()` function.
- Usually gets the most interesting findings from a security standpoint
- Structural flaws can often lead to business logic errors that may be hard to track or some unpredictable behaviours


**Dealing With False Positives and False Negatives**
- **False positives:** 
	- Reports on a vulnerability that isn't present in the code.
- **False negatives:** 
	- Doesn't report a vulnerability that is present in the code
- Happens if tool cannot correctly assess the target code 
	- Can happen **if we don't use** the tool correctly
- **Example** 
	- Three possible instances of SQL injection through manual review. 
	- One of them was discarded as character filtering was being applied to it effectively
		- Two confirmed SQL injection vulnerabilities. 
	- Psalm's output
		- Only one SQL injection is reported since it failed to understand about code `db_query()` being a wrapper to other database queries
	- Can use some **annotations** to give more context. 
		- Can specify that `db_query()` should be considered a sink, so we get an error if any tainted input reaches the function via the `$query` parameter. 
		- To do so, add the following comment on top of the `db_query()` function definition in `db.php`
			- `/**`
			- `* @psalm-taint-sink sql $query`
			- `* @psalm-taint-specialize`
			- `*/`
		- `@psalm-taint-sink` annotation 
			- Tells Psalm to check the `$query` parameter for tainted inputs of type `sql`. 
				- Now Psalm will issue a TaintedSQL error every time a tainted input reaches `db_query()`.
		- `@psalm-taint-specialize` annotation 
			- Tells Psalm that each invocation of the function should be treated as a separate issue and that the function's taintedness depends entirely on the inputs it receives.

End Result of using Psalm as a SAST tool

|       | Manual Review  | Psalm Review   | Verdict        |
| ----- | -------------- | -------------- | -------------- |
| $sql  | Vulnerable     | Vulnerable     | OK             |
| $sql2 | Not Vulnerable | Vulnerable     | False Positive |
| $sql3 | Vulnerable     | Not Vulnerable | False Negative |


> [!Question]
>  **What type of error occurs when the tool reports on a vulnerability that isn't present in the code?**

> [!Success] Answer
> False Positive

> [!Question]
>  **How many errors are reported after annotating the code as instructed in this task and re-running Psalm?**

Going to "db.php" to add annotations to the `db_query` function

![](/img/user/TryHackMe/THM_Images/1db5f93f7122d84ca657ce1b245c6827.png)

![](/img/user/TryHackMe/THM_Images/1948cb210f4345abc07b1b6a1e8b79f9.png)

![](/img/user/TryHackMe/THM_Images/367ffb4158b29cea946bc9869a23337e.png)

> [!Success] Answer
> 9

# Task 6 - SAST in the Development Cycle

- One of first tools to appear in cycle, around coding stage  
- **CI/CD integration:** 
	- SAST tools will check the code for vulnerabilities for each pull request or merge. 
	- Can execute SAST scans only at merges may help prevent slowdowns in the development pipeline
		- Avoids making all developers wait for full SAST scans.
- **IDE integration** 
	- SAST tools can be integrated into IDEs instead of waiting for a pull request or merge to occur. 
		- Fixes code as early as possible, saving time further ahead in the project.
- Can run SAST on both IDEs and CI/CD pipeline
	- IDE tools may run basic structural checks and enforce secure coding guidelines
	- CI/CD integrations may run more time-consuming dataflow/taint analysis.
- **Integrating SAST in IDEs**
	- **Psalm:**  
		- Will monitor in real-time and show same alerts as the console version directly into code.
		- Taint analysis won't be available
			- Only see the structural problems reported on a basic Psalm analysis.
	- **Semgrep:** 
		- Shows inline alerts directly in your code.
		- Can build custom rules if needed

> [!Task]
>  For this task's questions, we will analyse an old version of **ReciPHP**, a small open-source app. Before continuing, make sure to open the `reciphp.code-workspace` icon on your desktop. This will open a VS Code workspace where the project is already loaded for you. VS Code will take around 3 minutes to load, so be patient.

![](/img/user/TryHackMe/THM_Images/2cac9827f86e1c2453562edfd6e00944.png)

> [!Question]
>  **How many problems in total are detected by Semgrep in this project?**

![](/img/user/TryHackMe/THM_Images/830b7032f4fc5804a2c51d0f64c18096.png)

> [!Success] Answer
> 27

> [!Question]
>  **How many problems are detected in the `showrecipe.inc.php` file?**

![](/img/user/TryHackMe/THM_Images/88acff3d6415d71477e70b43a8a8948b.png)

> [!Success] Answer
> 8

> [!Question]
>  **Open showrecipe.inc.php. There are two types of problems being reported by Semgrep in this file. One is identified as "tainted-sql-string" and refers to possible SQL injections.
>  What other problem identifier is reported by Semgrep in this file? (Write the id reported by Semgrep)**

![](/img/user/TryHackMe/THM_Images/0ad4a9f9d4676194c185529336314df3.png)

Other than the "tainted-sql-string" error, the other error being shown is related for cross-site scripting.

> [!Success] Answer
> echoed-request

> [!Question]
>  **What type of vulnerability is associated with the problem identifier on the previous question?**

Refer to previous screenshot

> [!Success] Answer
> Cross-site Scripting
