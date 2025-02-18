---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/linux-system-hardening/","created":"2025-02-17T21:06:51.023-05:00","updated":"2025-02-18T14:34:53.475-05:00"}
---

# Task 2 - Physical Security

- Boot access  = root access
	- If threat actor can access system physically, they can use GRUIB (linux boot loader) to reset root password account
- Can set boot password through BIOS or UEFI
	- Only for personal devices, not servers
- Can add a GRUB password
	- `grub2-mkpasswd-pbkdf2`
	- Prompts input of password, generates hash
		- Prevents unauthorized users from resetting root password
	- Needs user to supply password to access boot configs via GRUB


> [!Question]
> **What command can you use to create a password for the GRUB bootloader?** 

> [!Success] Answer
> grub2-mkpasswd-pbkdf2

> [!Question]
> **What does PBKDF2 stand for?** 

![](/img/user/TryHackMe/THM_Images/Pasted image 20250217213800.png)

> [!Success] Answer
> Password-Based Key Derivation Function 2

# Task 3 - Filesystem Partitioning and Encryption

- LUKS (Linux Unified Key Setup)
	- Disk drive encryption scheme
	- Adds the following fields to the data when encrypting
		- LUKS phdr (LUKS partition header)
			- Stores info about UUID, cipher, key length/checksum
		- KM (Key material)
			- Split into multiple portions, each associated with a key slot
			- When active in the LUKS phdr, the KM section contains copy of master key encrypted with a users password
		- Bulk Data
			- Data encrypted by master key
				- Master key is saved/encrypted by users password in KM section

![](/img/user/TryHackMe/THM_Images/ee1310ecb1558e550a9bff3a53ece0ff.png)

- Pseudocode to encrypt data
	- `enc_data = encrypt(cipher_name, cipher_mode, key, original, original_length)`
- Key is derived from PKBDF2
	- `key = PBKDF2(password, salt, iteration_count, derived_key_length`
- Pseudocode to decrypt data
	- `original = decrypt(cipher_name, cipher_mode, key, enc_data, original_length)`
- Setting up LUKS
	- Install `cryptsetup-luks`. 
		- `apt install cryptsetup`
	- Confirm the partition name
		- `fdisk -l`, `lsblk` or `blkid`.
	- Set up the partition for LUKS encryption: 
		- `cryptsetup -y -v luksFormat /dev/sdb1`.
	- Create a mapping to access the partition 
		- `cryptsetup luksOpen /dev/sdb1 EDCdrive`.
	- Confirm mapping details
		- `ls -l /dev/mapper/EDCdrive`
		- `cryptsetup -v status EDCdrive`.
	- Overwrite existing data with zero 
		- `dd if=/dev/zero of=/dev/mapper/EDCdrive`.
	- Format the partition: 
		- `mkfs.ext4 /dev/mapper/EDCdrive -L "Strategos USB"`.
	- Mount it and start using it like a usual partition: 
		- `mount /dev/mapper/EDCdrive /media/secure-USB`.
- Check LUKS setting
	- `cryptsetup luksDump /dev/sdb1`
	- Gives UUID, cipher used, etc.



> [!Question]
> **What does LUKS stand for?** 

> [!Success] Answer
> Linux Unified Key Setup

> [!Question]
> **We cannot attach external storage to the VM, so we have created a `/home/tryhackme/secretvault.img` file instead. It is encrypted with the password `2N9EdZYNkszEE3Ad`. To access it, you need to open it using `cryptsetup` and then mount it to an empty directory, such as `myvault`. What is the flag in the secret vault?** 


![](/img/user/TryHackMe/THM_Images/Pasted image 20250217224912.png)

> [!Success] Answer
> THM{LUKS_not_LUX}

# Task 4 - Firewall

- Firewall decides which packets can enter or exit a system
- Can be either a host or a network firewall
- Linux firewall
	- Originally was a stateless firewall
		- Does not maintain info about ongoing TCP connections
	- Not possible to allow/deny packets based on process, only on port number
- Netfilter
	- Packet filtering software for linux kernel
	- Requires front end such as 
		- Iptables
			- CMD line tools to configure packet filtering rule set using netfilter hooks
			- Set of following default chains
				- Input
					- Packets incoming to firewall
				- Output
					- Packets outgoing from firewall
				- Forward
					- Packets routed through system
			- Example
				- `iptables -A INPUT -p tcp --dport 22 -j ACCEPT`
					- `dport`refers to destination port, 22
					- `-A` appends to a chain, in this case, `INPUT`
					- `-J` refers to jump to a target rule, in this case, `ACCEPT`
				- `iptables -A OUTPUT -p tcp --sport 22 -j ACCEPT`
					- `sport` refers to source port, 22
				- Does not come with a default deny policy, need to configure it for both chains
					- `iptables -A INPUT -j DROP`
					- `iptables -A OUTPUT -j DROP`
				- Need to apply the rules in the correct order,
					- Good to flush previous rules with `iptables -F`
		- nftables
			- Adds multiple improvements to iptables
			- Does not come with any default chains/tables, need to add manually
			- Example
				- `nft add table fwfilter`
					- Other commands like `add`, `delete`, `list`, `flush`
				- `nft add chain fwfilter fwinput { type filter hook input priority 0 \; }`
				- `nft add chain fwfilter fwoutput { type filter hook output priority 0 \;`
				- Can now add rules
				- `nft add fwfilter fwinput tcp dport 22 accept`
				- `nft add fwfilter fwoutput tcp sport 22 accept`
		- UFW (Uncomplicated Firewall)
			- Example
				- `ufw allow 22/tcp`
			- Easy to setup and use, front-end of a front-end
			- `ufw status` 
				- Shows settings, active rules
- Firewall policy
	- Need to decide on policy before configuring a firewall 
	- Two main approaches
		- Block everything and allow certain exceptions.
		- Allow everything and block certain exceptions.

> [!Question]
> **There is a firewall running on the Linux VM. It is allowing port 22 TCP as we can ssh into the machine. It is allowing another TCP port; what is it?** 

![](/img/user/TryHackMe/THM_Images/Pasted image 20250217230746.png)

> [!Success] Answer
> 12526

> [!Question]
> **What is the allowed UDP port?** 

Refer to screenshot above

> [!Success] Answer
> 14298

# Task 5 - Remote Access

- Common attacks against remote access include
	- Password sniffing
		- Credentials sent out the device unencrypted can be intercepted, leading to disclosure in password
		- Encrypt all traffic before leaving network
	- Password guessing / brute-force
		- Any device can try to connect to your server once SSH is enabled
		- Many users use easy to guess/weak passwords
		- Can disable login as root, only non-root users
		- Disable password authentication, user public key authentication instead
			- Use `ssh-keygen -r rsa` to create SSH key pair
				- Generates private key, `id_rsa`, and public key, `id_rsa.pub`
			- Use command `ssh-copy-id username@server` to copy public key to target SSH server
			- Double check `ssh_config` file to ensure that configurations are set
				-  `PubkeyAuthentication yes` to enable public key authentication
				- `PasswordAuthentication no` to disable password authentication
	- Can view SSH server config through `sshd_config` file
		- Located at `/etc/ssh/sshd_config`
	- Exploiting the listening service

> [!Question]
> **What flag is hidden in the `sshd_config` file?** 

![](/img/user/TryHackMe/THM_Images/Pasted image 20250217234041.png)

> [!Success] Answer
> THM{secure_SEA_shell}

# Task 6 - Securing User Accounts

- Using root account is very risky, can easily ruin system if improperly used
	- Needed for sys maintenance, install/remove software packages, update/configure system
- Can use a non-root account along with the `sudo` command to use root privileges
	- Account needs to be added to the sudoers group before using the command
	- `usermod -aG sudo username`
	- Can also disable root account afterwards
		- Modify `/etc/passwd` to change root shell to `/sbin/nologin`
		- `root:x:0:0:root:/root:/sbin/nologin`
- Can enforce a strong password policy through `libpwquality` library
	- Many options for password constraint
- Should also disable unused accounts
	- Can do it through setting shell of user account to `/sbin/nologin`
	- Can also do it for local services like `www-data`, `mongo`, `nginx`, etc.
		- Prevents RCE vulnerability since it can prevent interactive logins for the account of the service

> [!Question]
> **One way to disable an account is to edit the `passwd` file and change the account’s shell. What is the suggested value to use for the shell?** 

> [!Success] Answer
> `sbin/nologin`

> [!Question]
> **What is the name of the RedHat and Fedora systems sudoers group?** 

> [!Success] Answer
> wheel

> [!Question]
> **What is the name of the sudoers group on Debian and Ubuntu systems?** 

> [!Success] Answer
> sudo

> [!Question]
> **Other than `tryhackme` and `ubuntu`, what is the username that belongs to the sudoers group?** 

![](/img/user/TryHackMe/THM_Images/Pasted image 20250217235735.png)

> [!Success] Answer
> blacksmith

# Task 7 - Software and Services

- Any software can increase attack surface with a potential number of vulnerabilities
- Disable any unnecessary services
- Block unneeded network ports
- Avoid legacy protocols
- Remove identification strings
	- Ensure replies from server doesn't reveal information to attacker about what it is, version number, etc.

> [!Question]
> **Besides FTPS, what is another secure replacement for TFTP and FTP?** 

> [!Success] Answer
> SFTP

# Task 8 - Update and Upgrade Policies

- Keep all systems update with latest security patches/bug fixes
	- `apt update / upgrade`
	- `dnf/yum update`
- Use LTS (Long Term Support) releases of any OS
	- Ensure to run systems that can still receive security updates
- Consider updating kernel
	- Crucial to keep in check since any compromise is usually a major disaster in terms of damage
- Configure automatic updates
	- Prioritize stability over cutting-edge technology
- Take note of security news in case of vulnerability


> [!Question]
> **What command would you use to update an older Red Hat system?** 

> [!Success] Answer
> yum update

> [!Question]
> **What command would you use to update a modern Fedora system?** 

> [!Success] Answer
> dnf update

> [!Question]
> **What two commands are required to update a Debian system? (Connect the two commands with `&&`.)** 

> [!Success] Answer
> apt update && apt upgrade

> [!Question]
> **What does `yum` stand for?** 

> [!Success] Answer
> Yellowdog Updater, Modified

> [!Question]
> **What does `dnf` stand for?** 

> [!Success] Answer
> Dandified YUM

> [!Question]
> **What flag is hidden in the `sources.list` file?** 

![](/img/user/TryHackMe/THM_Images/Screenshot 2025-02-18 001707.png)

> [!Success] Answer
> THM{not_Advanced_Persistent_Threat}

# Task 9 - Audit and Log Configuration

- Can check in `/var/log` directory for various logs that can help for looking for threats
	- `/var/log/messages` - a general log for Linux systems
	- `/var/log/auth.log` - a log file that lists all authentication attempts (Debian-based systems)
	- `/var/log/secure` - a log file that lists all authentication attempts (Red Hat and Fedora-based systems)
	- `/var/log/utmp` - an access log that contains information regarding users that are currently logged into the system
	- `/var/log/wtmp` - an access log that contains information for all users that have logged in and out of the system
	- `/var/log/kern.log` - a log file containing messages from the kernel
	- `/var/log/boot.log` - a log file that contains start-up messages and boot information


> [!Question]
> **What command can you use to display the last 15 lines of `kern.log`?** 

> [!Success] Answer
> tail -n 15 kern.log

> [!Question]
> **What command can you use to display the lines containing the word `denied` in the file `secure`?** 

> [!Success] Answer
> grep denied secure
