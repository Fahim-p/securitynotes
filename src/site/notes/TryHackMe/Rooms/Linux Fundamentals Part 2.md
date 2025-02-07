---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/linux-fundamentals-part-2/","created":"2024-12-03T18:54:00.000-05:00","updated":"2025-02-06T21:54:06.497-05:00"}
---

# Task 3 - Introduction to Flags and Switches

- Commands without flags will run in default mode
	- Use flags to customize how it'll run
- **Man**
	- Manual page that shows all flags/switches available for said command (e.g ls)

> [!Question] 
**What directional arrow key would we use to navigate down the manual page?**

> [!Done] Answer
down

> [!Question] 
**What flag would we use to display the output in a "human-readable" way?**

![image1 3.png](/img/user/TryHackMe/THM_Images/47ed590eb3a52f1f9f729d4d7649882a.png)

> [!done] Answer
-h

# Task 4 - Filesystem Interaction Continued

- **Touch**
	- Create a blank file
	- Use echo or editors like nano to add content to it
- **Mkdir**
	- Create a folder
- **Cp**
	- Copy a file or folder
	- Two arguments
- **Mv**
	- Move a file or folder
	- Two arguments
	- Merges/modifies the second file given as an argument
	- Can also rename a file/folder
- **Rm**
	- Remove a file or folder
	- -R needed to remove directories
- **File**
	- Determine the type of a file
	- One argument

> [!question] 
**How would you create the file named "newnote"?**

> [!done] Answer
touch newnote

> [!Question] 
**On the deployable machine, what is the file type of "unknown1" in "tryhackme's" home directory?**

![image2 3.png](/img/user/TryHackMe/THM_Images/a91e2c62ae1b7fb2b3e4921a80b0d164.png)

> [!done] Answer
ASCII text

> [!Question] 
**How would we move the file "myfile" to the directory "myfolder"?**

> [!done] Answer
`mv myfile myfolder`

> [!Question] 
**What are the contents of this file?**

![image3 3.png](/img/user/TryHackMe/THM_Images/aa4135f5a51bd4b7ba486e73b4cf86f2.png)

> [!done] Answer
THM{FILESYSTEM}

# Task 5 - Permissions 101

- Execute, Read, Write (xrw)
- Separated into 3 columns; owner, group, user
**Ls -l**, Gives us permissions of all files

![image4 3.png](/img/user/TryHackMe/THM_Images/de86e102baab2441d7bc96cb0fddf829.png)

**Su**, Switches between users
- Need username and password
- **-l** switch
	- Start a shell that is much more similar to the actual user logging into the system
	- Inherit a lot more properties of the new user, i.e., environment variables

![image5 3.png](/img/user/TryHackMe/THM_Images/47a7db5991a6d5244fae58edb3bd5693.png)

> [!Question] 
**On the deployable machine, who is the owner of "important"?**

![image6 3.png](/img/user/TryHackMe/THM_Images/9907667e0a08e66cdf1f9478ce6a229e.png)

> [!done] Answer
user2

> [!Question] 
**What would the command be to switch to the user "user2"?**

> [!done] Answer
su user2

> [!Question] 
**Now switch to this user "user2" using the password "user2". Output the contents of "important", what is the flag?**

![image7 3.png](/img/user/TryHackMe/THM_Images/8202ac03f2e78b2c64250b435c2a38e6.png)

![image8 1.png](/img/user/TryHackMe/THM_Images/33f9719ad887d5a2ecb05fd6db9dea6f.png)

> [!done] Answer
THM{SU_USER2}
# Task 6 - Common Directories

**/etc**, Commonplace location to store system files

![image9 1.png](/img/user/TryHackMe/THM_Images/866aabf9e814764184096f04e76cf342.png)
        
**/var**, Stores data that is frequently accessed or written by services or applications running on the system

![image10.png](/img/user/TryHackMe/THM_Images/dd76ffb52e43830945518e60cee04dcc.png)
        
**/root**, Home for the "root" system user.

![image11.png](/img/user/TryHackMe/THM_Images/6a34c2800b22013d3ddb7a92a0f52c75.png)
    
**/tmp**
- Volatile and is used to store data that is only needed to be accessed once or twice
- Once the computer is restarted, the contents of this folder are cleared out
- Any user can write to this folder by default.
	- Once we have access to a machine, it serves as a good place to store things like our enumeration scripts.

![image12.png](/img/user/TryHackMe/THM_Images/589da78f9fdef9932b05d59ec8211e11.png)

> [!Question] 
**What is the directory path that would we expect logs to be stored in?**

> [!done] Answer
/var/log

> [!Question] 
**What root directory is similar to how RAM on a computer works?**

> [!Done] Answer
/tmp

> [!Question] 
**Name the home directory of the root user?**

> [!Done] Answer
/root