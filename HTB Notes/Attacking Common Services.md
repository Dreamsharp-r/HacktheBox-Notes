Attacking FTP

Common Services:
	- SMB        - TFTP         - Google Drive         - AWS S3
	- NFS         - SFTP         - OneDrive               - Azure Blob Storage
	- FTP          - Dropbox   - Sharepoint            - Google Cloud Drive

Common Tools used
	![[Pasted image 20240805140117.png]]
	

Attacking FTP
	-Performs file transfers, listing files, renaming, deleting, moving files and directories
	-Listens on port TCP/21 and port TCP/20 transfer data

Attack Flow
	1. Enumerate
		1. Run Nmap scans. 
			-sC inclueds ftp-anon script which checks for anonymous logins
		2. If ftp is open put in for username anonymous and no pw
		3. Once inside use commands:
			1.  get //downloads a single file
			2. mget // downloads multiple files
			3. put // upload a single file
			4. mput // uploads multiple files
			5. help // list commands
		4.  If user list and pw found then try brute forcing with credentials
			1.  Medusa or hydra
![[Pasted image 20240805101935.png]]

Attacking SMB
	- SMB is commonly used in Windows networks to share folders.
	- Interact w/ GUI, CLI, or tools
		- How to interact via GUI:
			- WINKEY + R and enter in the file share path
		-How to interact via CLI:
			- dir \\[filepath]
			- net use [drive letter]: \\[filepath]   \\ connect to shared resource
			![[Pasted image 20240805121454.png]]
			Providing Username & Password
			![[Pasted image 20240805121945.png]]

			![[Pasted image 20240805122315.png]]

Creating Scripts in cmd:
	dir [drive]:\*cred* /s /b
			/s = display files in a specified directory and all subdirectories
			/b = Use bare format (no heading information)
			![[Pasted image 20240805122722.png]]
			.
			How to interact via Powershell:
					Finding the directory
				
				![[Pasted image 20240805123710.png]]
				Connecting to an existing drive
				![[Pasted image 20240805123858.png]]
				![[Pasted image 20240805123948.png]]



![[Pasted image 20240805101558.png]]

Additional techniques
	-finding an ssh key if downloaded will require you to change the permissions inorder to utilize it
		-Utilize cmd:  chmod 600 [ssh key]
	-Utilizing crackmapexec has additional flags
		-using flag --continue-on-success // will continue spraying
		- --local-auth // used on non-domain joined computers	


Attacking SQL Databases
	- SQL relational databases
		- MySQL
			- GUI: the GUI to interact with MySQL is MySQL Workbench
			- CLI: mysql, mysql.exe
			- port TCP/3306 and in 'hidden' mode uses TCP/2433
		- MSSQL
			- GUI:
			- CLI: sqsh, sqlcmd
			- port TCP/1433 and UDP/1434
	- NoSQL databases
	- Hierarchical databases
			- GUI for all databases use dbeaver
			 ![[Pasted image 20240805133605.png]]
			 

![[Pasted image 20240805101630.png]]

![[Pasted image 20240805101716.png]]

The default schemas for MySQL and MSSQL
![[Pasted image 20240820185942.png]]

Capturing MSSQL Service Hash is the ideal way to get access into other databases
	-Use the command listed above for hash stealing but input the IP of your target
	- In another window type in the cmd
			- sudo impacket-smbserver share ./ -smb2support
			- This will capture the NTLM hash of your target


Attacking RDP
	- Best way to get in is to perform Password Spraying. Works by attempting a single password for many usernames before trying another password, this avoid account lockout
		- Crowbar tool
		- Hydra tool
	Different RDP systems:
			- rdesktop
			- xfreerdp
	Hijacking other users:
			1. If another user is connected via RDP to the compromised machine you can hijack their session
					- Open Powershell (PS) and type in query user to find listing of RDP users
					- Command sc.exe create sessionhijack binpath= "cmd.exe /k tscon 4 /dest:rdp-tcp#13"
					- net start sessionhijack
					- This method no longer works on Server 2019
			2. If somehow you acquire the hash of another user it can used in conjunction w/ xfreerdp to log in
					- Restricted Admin Mode must be enabled on the target host
					- Add a new reg key DisableRestrictedAdmin under HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa



![[Pasted image 20240805101739.png]]
Attacking DNS



![[Pasted image 20240805101759.png]]
1. Perform a Nmap sweep
2. Perform a zone transfer w/ dig AXFR
	1. Tools exist as well. 
		1. Fierce // perform enumeration on all DNS servers of the root domain for zone transfers
		2. ![[Pasted image 20240902133855.png]]

3. To perform subdomain enumeration sweeps use these tools:
	1. Subbrute
	2. Subfinder

Attacking Email Services



![[Pasted image 20240805101813.png]]
