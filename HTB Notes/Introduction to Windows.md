   

Introduction to Windows

Major Windows OS and Vs. number  
![d762a73595decaac26a6de1f1b92f28a.png](16f8a901fa7e4f99b5292825517cb7ef.png)

Directory Structure of the Windows OS  
![a1e96fb1730a68387331aad406721ab4.png](26c39f86c2764724b5d2dcd35618fb7c.png)

Common Remote Access Technologies  
![414236e64e4f619d2f357b686fe00675.png](c8e17aee048d4758a6e64c4c657d05b7.png)

- Module utilize RDP.
    - Windows has a built-in RDP client alled Remote Desktop Connection (mstsc.exe)
    - For the connection to work make sure to allow remote access on Windows
    - Linux tool for RDP is xfreerdp
    - Add to the command /dynamic-resolution to resize the window  
        ![a14d150f7fb2108d1d381547530466f2.png](2665832583884843a5dc15290ccc1151.png)

FAT32 Pro/cons  
![f35cdefaa83b1131aaf0b9632df87abb.png](aee5ee15789442199c7ce2eaeb814e23.png)

NTFS (New Technology File System)  
![fd297fae4d52824447636cd3298024b6.png](272290d9ec774a348a711d167b17822f.png)

NTFS permissions on specific directories  
![6629e1962f370c003002f83694290f02.png](c1e1d324cac347f9aba93b988d53d579.png)

Command List  
![1f92915fe04c88c7045adcebc1e8a7f7.png](2041e2c6cf6b41eab36b7c13472efb13.png)  
![51b1f46f082fd18a1fc8fbb857996380.png](e09081c855294a189a5df8670fedcfe3.png)

Get-WmiObject  
![a4b7f97cf763b9f6b6618728f2758c8b.png](07e108598277479ab352bacf34d0a8db.png)

- Find information about the operating system
- List itemUsed also w/ Get-WmiObject is:
    - Win32_Process = process listing
    - Win32_Service = Services listing
    - Win32_Bios = BIOS information

dir c:\ /a command  
![ce1991fcf40da8cf15cef7bd5582768f.png](117322ed944a4673be987abdf12f0638.png)

tree command  
![f8feba182648a0fb6d534b51c390baed.png](bf1f26d547924237914c86528db67e66.png)

- tree c:\ /f | more
    
    - Allows you to walk through all the filees within the C drive one screen at a time.
- wmic useraccount get name,sid = allows you to get the SID of users.
    
    - Switch out useraccount for group