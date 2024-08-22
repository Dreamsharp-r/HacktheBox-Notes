   

Detecting Windows Attacks with Splunk

**Detecting Attacks within Windows Event Logs**

Key Terms:  
Kerberos is a network authentication protocol used to securely authenticate users and services within a AD environment.  
(Client) -> (Request TGT) -> (KDC) -> (Verifies info) -> (Issue TGT encrypted w/ user secret key) Valid for a specific period  
(Client) -> (Request TGS-REQ utilizing TGT) -> (KDC) -> (validates TGT) -> (Issues TGS)

EventCode = Sysmon  
Event IDs = Windows Security log events  
Detecting Common User/ Domain Recon  
Common Tools:

- BloodHound // executes numerous LDAP queries directed at the DC aiming to amass information about the domain
- SharpHound

Common commands:

- whoami /all
- wmic computersystem get domain
- net user /domain
- net group "Domain Admins" /domain
- arp -a
- nltest /domain_trusts

Within Splunk to detect Domain recon:  
`index=main source="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" EventID=1 earliest=1690447949 latest=1690450687 | search process_name IN (arp.exe,chcp.com,ipconfig.exe,net.exe,net1.exe,nltest.exe,ping.exe,systeminfo.exe,whoami.exe) OR (process_name IN (cmd.exe,powershell.exe) AND process IN (*arp*,*chcp*,*ipconfig*,*net*,*net1*,*nltest*,*ping*,*systeminfo*,*whoami*)) | stats values(process) as process, min(_time) as _time by parent_process, parent_process_id, dest, user | where mvcount(process) > 3`

Within Splunk to detect BloodHound  
`index=main earliest=1690195896 latest=1690285475 source="WinEventLog:SilkService-Log" | spath input=Message | rename XmlEventData.* as * | table _time, ComputerName, ProcessName, ProcessId, DistinguishedName, SearchFilter | sort 0 _time | search SearchFilter="*(samAccountType=805306368)*" | stats min(_time) as _time, max(_time) as maxTime, count, values(SearchFilter) as SearchFilter by ComputerName, ProcessName, ProcessId | where count > 10 | convert ctime(maxTime)`

- Search Filter is _(samAccountType=8053606368)_ because it searches for events related to LDAP queries

---

Detecting Password Spraying

Common Tools

- Spray

Event IDs

- 4625 - Failed Logon  
    ![5ae805376ea238f6fc642299e5f7bf53.png](c8f772eb4d5c43ae850ac452c944d02a.png)

Within Splunk to detect Password Spraying  
`index=main earliest=1690280680 latest=1690289489 source="WinEventLog:Security" EventCode=4625 | bin span=15m _time | stats values(user) as Users, dc(user) as dc_user by src, Source_Network_Address, dest, EventCode, Failure_Reason`

---

Detecting Responder-like Attacks

- LLMNR (Link-local Multicast Name Resolution) and NBT-NS (NetBIOS Name Service) poisoning
- Both used to resolve hostnames to IPs on local networks when FQDN fails.  
    ![41dac459e8bf4ab5dc8028464e73eb97.png](2c33e526859a432a8e31f7fb8ef63424.png)  
    Common Tools
- Responder

Within Splunk to detect Responder-like Atacks  
`index=main earliest=1690290078 latest=1690291207 SourceName=LLMNRDetection | table _time, ComputerName, SourceName, Message`

Utilize Event ID 22  
`index=main earliest=1690290078 latest=1690291207 EventCode=22 | table _time, Computer, user, Image, QueryName, QueryResults`

Utilizing Event code 4648  
`index=main earliest=1690290814 latest=1690291207 EventCode IN (4648) | table _time, EventCode, source, name, user, Target_Server_Name, Message | sort 0 _time`

---

Detecting Kerberoasting

Common Tools:

- Rubeus

Event IDs  
![6c688682ca5c3b9f6a4b26995eb086a4.png](7fcb2fda9c674090a3af5de8f32dc4a0.png)

- 4648 (a logon was attempted using explicit credentials)  
    Kerberos Authentication Process  
    ![e735e74407e1552972fccc4948f59850.png](f98e3277a5ff4dc28d1f9de47237d33b.png)  
    ![d1add5b3c526d7b6172b0a0333ff07ff.png](afe83c31544f4011844c85da14c814b5.png)

Within Wireshark this traffic would be observed:  
![3b79bd4caf05c21018f37179172fae83.png](e0f7dccc5dcb4adaa8ffde68fa856edc.png)

Within Splunk to detect Kerberoasting - Benign TGS Requests  
`index=main earliest=1690388417 latest=1690388630 EventCode=4648 OR (EventCode=4769 AND service_name=iis_svc) | dedup RecordNumber | rex field=user "(?<username>[^@]+)" | table _time, ComputerName, EventCode, name, username, Account_Name, Account_Domain, src_ip, service_name, Ticket_Options, Ticket_Encryption_Type, Target_Server_Name, Additional_Information`

Within Splunk to detect Kerberoasting - SPN Querying  
`index=main earliest=1690448444 latest=1690454437 source="WinEventLog:SilkService-Log" | spath input=Message | rename XmlEventData.* as * | table _time, ComputerName, ProcessName, DistinguishedName, SearchFilter | search SearchFilter="*(&(samAccountType=805306368)(servicePrincipalName=*)*"`

Within Splunk to detect Kerberoasting - TGS Requests  
`index=main earliest=1690450374 latest=1690450483 EventCode=4648 OR (EventCode=4769 AND service_name=iis_svc) | dedup RecordNumber | rex field=user "(?<username>[^@]+)" | bin span=2m _time | search username!=*$ | stats values(EventCode) as Events, values(service_name) as service_name, values(Additional_Information) as Additional_Information, values(Target_Server_Name) as Target_Server_Name by _time, username | where !match(Events,"4648")`

Within Splunk to detect Kerberoasting using Transactions - TGS Requests

- Transaction command groups events into transactions based on specified fields and criteria
- Focuses on identifying events with EventCode 4769 that are part of an incomplete transaction. i.e. not ending with EventCode 4648 w/n 5-second window

Detecting AS-REPRoasting  
![fbd3184f93662a6f7ea79874f6b8309a.png](f215b785b5c542f9aa4ab04ca0b676df.png)

Event IDs  
4768 (TGT Request) contains a PreAuth Type attribute indicating pre-authentication is enabled

Within Splunk to detect AS-REPRoasting - Querying Accounts w/ Pre-Auth disabled  
`ndex=main earliest=1690392745 latest=1690393283 source="WinEventLog:SilkService-Log" | spath input=Message | rename XmlEventData.* as * | table _time, ComputerName, ProcessName, DistinguishedName, SearchFilter | search SearchFilter="*(samAccountType=805306368)(userAccountControl:1.2.840.113556.1.4.803:=4194304)*"`

Within Splunk detecting AS-REPRoasting - TGT Request for Accounts with Pre-Auth Disabled  
`index=main earliest=1690392745 latest=1690393283 source="WinEventLog:Security" EventCode=4768 Pre_Authentication_Type=0 | rex field=src_ip "(\:\:ffff\:)?(?<src_ip>[0-9\.]+)" | table _time, src_ip, user, Pre_Authentication_Type, Ticket_Options, Ticket_Encryption_Type`

---

Detecting Pass-the-Hash  
![1b2224b5337cc91ed544b4549e49ac3c.png](3680694382204ad8bcaf31610eda1e9e.png)  
Common Tools:  
Mimikatz - Extract NTLM hash of a user

Commands:  
runas // allows a user to execute commands as another user

- ![afd1b50871914781f7a133cd60991c1e.png](72fc0731bf294391a71d48357d4fb207.png)

Event IDs  
4624 (Logon) w/ LogonType 2 (interactive)  
4624 (Logon) w/ LogonType 9 (NewCredentials)  
Detecting Pass-the-Hash  
`index=main earliest=1690450708 latest=1690451116 source="WinEventLog:Security" EventCode=4624 Logon_Type=9 Logon_Process=seclogo | table _time, ComputerName, EventCode, user, Network_Account_Domain, Network_Account_Name, Logon_Type, Logon_Process`

Adding LSASS memory Access to the Detection  
`index=main earliest=1690450689 latest=1690451116 (source="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" EventCode=10 TargetImage="C:\\Windows\\system32\\lsass.exe" SourceImage!="C:\\ProgramData\\Microsoft\\Windows Defender\\platform\\*\\MsMpEng.exe") OR (source="WinEventLog:Security" EventCode=4624 Logon_Type=9 Logon_Process=seclogo) | sort _time, RecordNumber | transaction host maxspan=1m endswith=(EventCode=4624) startswith=(EventCode=10) | stats count by _time, Computer, SourceImage, SourceProcessId, Network_Account_Domain, Network_Account_Name, Logon_Type, Logon_Process | fields - count`

---

Detecting Pass-the-Ticket

- lateral movement technique
- Instead of using NTLM hashes, it abuses and leverages the Kerberos TGT and TGS tickets to authenticate to other systems to access network resources without needing to know the users' password.

Common Tools:  
Mimikatz  
Rubeus

Event IDs:  
4648 (Explicit Credential Logon Attempt)  
4624 (Logon) Successful logon to the system  
4672 (Special Logon) logon w/ special previliges such as running app as admin  
4768 (Kerberos TGT Request)  
4769 (Kerberos Service Ticket Request)

Detecting Pass-the-Ticket w/ Splunk  
`index=main earliest=1690392405 latest=1690451745 source="WinEventLog:Security" user!=*$ EventCode IN (4768,4769,4770) | rex field=user "(?<username>[^@]+)" | rex field=src_ip "(\:\:ffff\:)?(?<src_ip_4>[0-9\.]+)" | transaction username, src_ip_4 maxspan=10h keepevicted=true startswith=(EventCode=4768) | where closed_txn=0 | search NOT user="*$@*" | table _time, ComputerName, username, src_ip_4, service_name, category`

---

Detecting Overpass-the-Hash (Pass-the-key)  
Leverages stolen pw hashes to obtain TGTs. Allows authentication to occur via Kerberos rather than NTLM

Common Tools  
Mimikatz  
Rubeus

Event ID:  
4768 (Kerberos TGT Request) w/ (TCP/UDP port 88)

Detecting Overpass-the-Hash w/ Splunk (Targeting Rubeus)  
`index=main earliest=1690443407 latest=1690443544 source="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" (EventCode=3 dest_port=88 Image!=*lsass.exe) OR EventCode=1 | eventstats values(process) as process by process_id | where EventCode=3 | stats count by _time, Computer, dest_ip, dest_port, Image, process | fields - count`

---

Detecting Golden Tickets & Silver Tickets  
Attacker forges a TGT to gain unauthorized access to a AD as a domain admin.  
Long validity period until its expired or revoked

Common Tools:  
Mimikatz w/ a DCSync Attack

Detecting this attack relies on how the NTLM hash is extracted from the AD

- DCSync Attack
- NTDS.dit file access
- LSASS memory read on the DC (Sysmon Event ID 10)

Event Codes:  
4768 (Kerberos TGT Request)  
4769 (Kerberos Service Ticket Request)  
4770 (Kerberos service ticket was renewed)

Detecting Golden Tickets w/ Splunk  
`index=main earliest=1690451977 latest=1690452262 source="WinEventLog:Security" user!=*$ EventCode IN (4768,4769,4770) | rex field=user "(?<username>[^@]+)" | rex field=src_ip "(\:\:ffff\:)?(?<src_ip_4>[0-9\.]+)" | transaction username, src_ip_4 maxspan=10h keepevicted=true startswith=(EventCode=4768) | where closed_txn=0 | search NOT user="*$@*" | table _time, ComputerName, username, src_ip_4, service_name, category`

---

Silver Ticket  
Forges a TGS ticket for a targeted service account (e.g. SharePoint, MSSQL). More limited in scope as they only allow access toa specific resource

Common Tools  
Mimikatz

Event ID  
4720 (A user account was created)  
4672 (Special Logon)

Detecting Silver Tickets w/ Splunk through User Correlation

![b35b36a8bfa0df0f3e7d3a2edeee2a1e.png](9d8b4f96ba024dd0b2aa8e846886839b.png)  
`index=main latest=1690545656 EventCode=4624 | stats min(_time) as firstTime, values(ComputerName) as ComputerName, values(EventCode) as EventCode by user | eval last24h = 1690451977 | where firstTime > last24h ```| eval last24h=relative_time(now(),"-24h@h")``` | convert ctime(firstTime) | convert ctime(last24h) | lookup users.csv user as user OUTPUT EventCode as Events | where isnull(Events)`

Detecting Silver Tickets w/ Splunk by targeting Special Privileges Assigned to New Logon  
`index=main latest=1690545656 EventCode=4672 | stats min(_time) as firstTime, values(ComputerName) as ComputerName by Account_Name | eval last24h = 1690451977 ```| eval last24h=relative_time(now(),"-24h@h") ``` | where firstTime > last24h | table firstTime, ComputerName, Account_Name | convert ctime(firstTime)`

---

Detecting Unconstrained Delegation & Contrained Delegation Attacks

Unconstrained Delegation is a privilege that can be granted to User Account or Computer Account in an AD allowing a service to authenticate to another resource on behalf of any user. EX. Web server need access to DB server to make changes on user's behalf

Common Tools  
Mimikatz

Event IDs  
4104 (execution of a remote Powershell Command)

Detecting Unconstrained Delegation Attacks w/ Splunk  
`index=main earliest=1690544538 latest=1690544540 source="WinEventLog:Microsoft-Windows-PowerShell/Operational" EventCode=4104 Message="*TrustedForDelegation*" OR Message="*userAccountControl:1.2.840.113556.1.4.803:=524288*" | table _time, ComputerName, EventCode, Message`

---

Constrained Delegation  
Feature in AD that allows services to delegate user credentials only to specified resources. Any user that have service principal names (SPNs) set in their msDS-AllowedToDelegateTo property can impersonate any user in the domain to those specific SPNs.

Detecting Constrained Delegation Attacks w/ Splunk  
`index=main earliest=1690544553 latest=1690562556 source="WinEventLog:Microsoft-Windows-PowerShell/Operational" EventCode=4104 Message="*msDS-AllowedToDelegateTo*" | table _time, ComputerName, EventCode, Message`

Detecting Constrained Delegationn Attacks - Leveraging Sysmon Logs  
`index=main earliest=1690562367 latest=1690562556 source="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" | eventstats values(process) as process by process_id | where EventCode=3 AND dest_port=88 | table _time, Computer, dest_ip, dest_port, Image, process`

---

Detecting DCSync & DCShadow  
A technique by which using the AD Domain Controller permission to grant DC to read all objects including password hashes (Replication Directory Changes)

Event ID  
4662 DS-Replication-Get-Changes w/ property {1131f6aa-9c07-11d1-f79f-00c04fc2dcd2}

Detecting DCSync w/ Splunk  
`index=main earliest=1690544278 latest=1690544280 EventCode=4662 Message="*Replicating Directory Changes*" | rex field=Message "(?P<property>Replicating Directory Changes.*)" | table _time, user, object_file_name, Object_Server, property`

---

DCShadow  
An advanced tactic used to enact unauthorized alterations to AD objects, encompassing the creation or modification of objects w/o producing standard security logs. Uses the Directory Replicator (Replicating Directory Change) permission.

Event ID  
4742 (Computer Account was changed)

Detecting DCShadow w/ Splunk  
![a2c6cbb05730f9b4c31f91157308e01e.png](4dd2c43a36864dc999cd5a0c9a39d3cd.png)  
`index=main earliest=1690623888 latest=1690623890 EventCode=4742 | rex field=Message "(?P<gcspn>GC\/[a-zA-Z0-9\.\-\/]+)" | table _time, ComputerName, Security_ID, Account_Name, user, gcspn | search gcspn=*`