   

Using the Metasploit Framework

MSFconsole commands

- msfconsole -q // Start up metasploit w/o displaying the banner
- sudo apt update && sudo apt install metasploit-framework // update the metasploit framework
- help search // gives the parameters to search metasploit framework
- show payloads // list all payloads
- show encoders // list all compatiable encoding schemes  
    ![222332e703b9e4be32d8dcba246f18bb.png](13029c0d07c741a2959190b739bebe02.png)  
    ![c7a38ddcd58b4d57e537f753d69b97d3.png](45fb54117d4c4a959483e29bd9e3a896.png)  
    ![2906c77c7b18ea768643b6ccbdc70e9c.png](4c60939a13b84aadbb3a8a6632ca4f09.png)

---

Meterpreter Commands  
![801919b42cd98aa473c8e5469bf6eacd.png](57b69f54483f45cdb17a3677794fd3a0.png)  
![5bb1225f7410d9609b37742f9035574d.png](8fb3201797f84bf98763382b255e5fcc.png)

---

![ad54f679add77ee5f8e696c2b813bb6d.png](3c8f9862e1ac4644975c326fbeabed9c.png)

- Enumeration
    - Passive Scanning
        - OSINT
        - Whois/ DNS records
    - Active Scanning
        - nMAP / Nessus / NexPose Scans / openVAS
        - Web Service Identification Tools
    - Vulnerability Research
        - VulnDB (GUI)
        - Rapid7 (GUI)
        - SearchSploit (CLI)
        - Google Dorking
- Preparation
    - Importing custom modules
    - Code Auditing
- Exploitation
    - Run modules locally
- Privilege Escalation
    - Vulnerability Research
    - Credential Gathering
    - Token impersonation
- Post-Exploitation
    - Pivoting to other systems
    - Data Exfiltration
    - Cleanup

---

Navigating Msfconsole

- Metasploit Modules follow this syntax
    
- [No.] [type]/[os]/[service]/[name]
    
- [0][exploit]/[windows]/[smb]/[ms17_010_psexec]  
    ![94485cc5ed68e68da0ff89b5950ef06d.png](6890a8ebedda47a686d21f5f35a44b4c.png)
    
- Specific Searching
    
- Search via keywords or by the name of the exploit  
    ![b859a378cba56e96801878555699b806.png](9671b25171154e078dffb77e5363e5cb.png)  
    ![3dadaa762ff0ce1fce992e8ae6b6404d.png](12f41c7f8c7f4c62a2eadf25933daaaa.png)
    

---

Encoding Schemes  
![6cb7b113ebd16ccbb9d10348b40f4c18.png](054d1535d8d941269d1a6f9eb3074638.png)

- msfvenom does both payload generation and Encoding  
    ![5d589e929d5ba1577da85b72c6798c43.png](ae523d3e629b473b817fcf44f8a34a87.png)  
    ![9630d4e46471d1e81b633c4ab73ae9d9.png](80e8216f78004c1bb4c04ae0820ae96e.png)
- With encoding add
    - -e x86/shikata_ga_nai  
        ![e3ecbbe6efd3b5f94b60b0758476f979.png](9e1822908dcb4e76a03d70f76afc3d2b.png)  
        ![433a1a9e57b104014cc26ce209156017.png](17d2ee1ef00548cf93898fdbab4fd463.png)
- Creates an executable called TeamViewerInstall.exe

Tracking Status with Databases  
![99f94f8214c276037aec6b8dd4c54399.png](5c671980fbff4133b1deeee9855a5910.png)

1. sudo service postgresql status

- Check the status of PostgreSQL

2. sudo systemctl start postgresql

- Starts the PostgreSQL

3. sudo msfdb init

- Initiates a Database  
    NOTE: ![721da6a8c329c3b22663003ab0776966.png](f6717e34ffbe4f2bbf319e59e230d5a3.png)

4. sudo msfdb run

- Connect to the Initiated Database

5. help database

- Displays all the commands