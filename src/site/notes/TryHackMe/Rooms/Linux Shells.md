---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/linux-shells/","created":"2024-12-09T19:20:00.000-05:00","updated":"2025-03-11T00:32:59.257-04:00"}
---

# Task 2 - How to Interact With a Shell?

- Bash (Bourne Again Shell) is usually the default shell given
- Basic commands
	- `Pwd`
	![](/img/user/TryHackMe/THM_Images/9be34534f727957341cfb4b25c5d9180.png)
	- `cd`
	![](/img/user/TryHackMe/THM_Images/5e0d9e4478aded1051088e2ead8121d0.png)
	- `ls`
	![](/img/user/TryHackMe/THM_Images/4f76fa593b61952e9ac962aca8f83d65.png)
	- `cat`
	![](/img/user/TryHackMe/THM_Images/4f76fa593b61952e9ac962aca8f83d65.png)
	- `grep`
	![](/img/user/TryHackMe/THM_Images/787df88be20b1c801cc481dd480538db.png)

> [!Question] 
>**What is the default shell in most Linux distributions?**

> [!Success] Answer
> Bash

> [!Question] 
> **Which command utility is used to list down the contents of a directory?**

> [!Success] Answer
 >ls

> [!Question] 
 > **Which command utility can help you search for anything in a file?**

> [!Success] Answer
> grep
# Task 3 - Types of Linux Shells

- `Echo $SHELL`
	- Shows the shells that currently in use
	![image6 7.png](/img/user/TryHackMe/THM_Images/d3d56c551f70e7cc2a52ffe0119ffb31.png)
	- Can cat /etc/shells to show all available shells
	![image7 7.png](/img/user/TryHackMe/THM_Images/08329640ea67c154f8d57183755e6ba6.png)
	- Type shell name to change between them
	![image8 5.png](/img/user/TryHackMe/THM_Images/a12f3bd2f7191de907f50317b9a1326c.png)

- **Bash Shell**
	- Default shell for most linux distributions
	- Has capabilities from previous shell iterations, all in one
	- Scripting capabilities
	- Tab completion
	- History file and logs all commands
- **Fish Shell**
	- Simple syntax
	- Auto spell correction
	- Syntax highlighting
	- Scripting, tab completion, and command history
- **Z Shell**
	- Advanced tab completion, script writing
	- Auto spell correction
	- Slower due to extensive customization
	- Command history, more features

> [!Question] 
> **Which shell comes with syntax highlighting as an out-of-the-box feature?**

> [!Success] Answer
> FISH

> [!Question] 
> **Which shell does not have auto spell correction?**

> [!Success] Answer: 
> Bash

> [!Question] 
> **Which command displays all the previously executed commands of the current session?**

> [!Success] Answer
> History
# Task 4 - Shell Scripting and Components

- .sh needed to create bash script files
    ![image9 5.png](/img/user/TryHackMe/THM_Images/88883384e9c619026ae0bbbfe83602cb.png)
- **Shebang**
	- Used at the beginning of every bash script, with `#!`
	- Defines the interpreter
	![image10 4.png](/img/user/TryHackMe/THM_Images/46ae7cc88a2d3fd22297d2c266f9cacc.png)
- **Variables**
	- `Read`
		- Takes input from the user
		- Used alongside a new variable name to put the input into that variable
	- `$`
		- Used beside the variable name to call it during print statements or other functions
- Example
        ![image11 4.png](/img/user/TryHackMe/THM_Images/3891227dafbc2601e70b01fc904675e4.png)   
- **chmod**
	- Changes permissions of a file
		- Used in this context to make the script have execution permissions
		- Example,
		![image12 4.png](/img/user/TryHackMe/THM_Images/22083642075a3c0fe1d3c0eb92b6aec2.png)
- **./**
	- Tells the shell to execute file present in current directory
		- Of not used, then it'll search for script in PATH environment variable
			- Usually generates an error
	- Example
	![image13 3.png](/img/user/TryHackMe/THM_Images/e3480b3e5b2369ec637ae74b7825b4d5.png)
- **Loops**
	- Variable `i` is used as a iterator, starts from first number to last number incrementally
	- `Do`
		- Indicates start of loop code
	- `Done`
		- Indicates end of code
	- Example
        ![image14 3.png](/img/user/TryHackMe/THM_Images/350d4879ee2e7cf34cb82d72060a023e.png)
- **Conditional Statements**
	- `If`
		- Staring condition, checks for a set of conditions,
		- If it matches, then it'll run the commands beneath it with the **then**.
		- If it does not match, then it'll skip to **else** if its defined
			- If else is not defined, then it skips to **fi**
	- Example
        ![image15 3.png](/img/user/TryHackMe/THM_Images/fd1c30b25f9e53139612fccd784f0dfa.png)
- **Comments**
	- Done with `#` with a space afterwards
        ![image16 3.png](/img/user/TryHackMe/THM_Images/88028db6e7f4a023f2817dfa0639da67.png)
        
> [!Question] 
> **What is the shebang used in a Bash script?**

> [!Success] Answer
> #!/bin/bash

> [!Question] 
**Which command gives executable permissions to a script?**

> [!Success] Answer
chmod +x

> [!Question] 
> **Which scripting functionality helps us configure iterative tasks?**

> [!Success] Answer
loops

# Task 6 - Practical Exercise

- Script given that searches for a specific keyword in all files (.log files) in a specified directory
- Need to modify script in order to make it correctly run
- Given information from the question
	- Flag: thm-flag01-script
	- Directory: /var/log

Opening console, can see that the script "flag hunt.sh" is given in the /home/user directory, can open it with nano

![image17 3.png](/img/user/TryHackMe/THM_Images/1b30e4b244eaced0e14b1399b20e934b.png)

Opening up file shows us that the "directory" and "flag" variables are empty, need to fill out.

![image18 3.png](/img/user/TryHackMe/THM_Images/0c680ae9ac0b69925981f57608336f2c.png)

Filled out both variables, noticed that the for loop has a empty quotations, need to fill out

![image19 3.png](/img/user/TryHackMe/THM_Images/845cb0029d5e64128e7a08549bfe0bea.png)

Filled it out with the directory variable.

![image20 3.png](/img/user/TryHackMe/THM_Images/83f46079b6df28b7bc5b8ec42d149ae4.png)

Ensured to save it with Ctrl + X and then "Yes" to save it. Then ran the script.

![image21 3.png](/img/user/TryHackMe/THM_Images/76dcf358903f520edb0309c8d18a6a2f.png)

> [!Question] 
**Which file has the keyword**?

> [!Success] Answer
authentication.log

> [!Question] 
**Where is the cat sleeping?**

![image22 2.png](/img/user/TryHackMe/THM_Images/9916d8fd2fdfc77965b0cdef3099272a.png)

> [!Success] Answer
Under the table