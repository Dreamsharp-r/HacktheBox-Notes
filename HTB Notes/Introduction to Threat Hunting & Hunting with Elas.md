   

Introduction to Threat Hunting & Hunting with Elastic

![1931eb34452bafd03a8e185f3acaea5c.png](bdb3141508dc4da2a95d6abd4c59f6f9.png)

![0c3c274dc75a24208e0238b3214cbbf3.png](96ed33dce7bc49438579e4dae2d205a4.png)

When Should we Hunt?

- Multiple network anomalies are detected
- New IOCs or new information comes to light
- During an Incident Response (IR)
- Periodic proactive hunts

Threat Hunting Process:  
1. Initial phase is about planning preparation  
2. Forumlating a hypothesis  
3. Designing the Hunt  
4. Data gathering and Examination  
5. Evaluating Findings and Testing Hypothesis  
6. Mitigating Threats  
7. Continous Learning and Enhancements

Intelligence Types

- Strategic
- Operational
- Tactical

![0b9ab5ce9192b5b5e2484895f1948c5f.png](29d7f92bd0dc4f78b01260473279d154.png)  
![2b84fbf1ac5c8b2a8f21a30749371f54.png](ff1bfcc22e2d499eaa3c0ddb2695ebc9.png)  
![6016d7a6ca3db1fa523f8d12d3f75e67.png](2aae4489cfd741f7b95e83001b95df25.png)

Validating Information on a Report

- Group IOCs based on Network based (IPs, domains), Host based (File hashes, registry keys) and email based (email addresses, subject lines), lastly specific patterns such as HTTP headers.

Understanding Elastic  
![4749b25fe408bc2bc31802b5e5aae389.png](d0661bcce0f54305939c7b188bcc74d3.png)

- Understand Sysmon Event IDs
    - [https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon "https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon")
- Use wild card to find all instances of a file
    - EX. file.name:*invoice.one
- Note Timestamps and correlate the data with the process.name or process executable
- Downloaded files run under sysmon Event ID 11 (File Create)
    - EX. event.code:11 AND file.name:invoice.one*
- Correlate more data. Note the host, source.ip, and network connection
    
    - EX. Sysmon Event ID 3 (Network connection)  
        _Sysmon might have no entries. Try Zeek logs  
        -Zeek Query. Source.ip [8.8.8.8] AND dns.question.name:_  
        ![cefd536ce794df8bcf93654d42439c7a.png](9f85667e1550472a90aa4d9d33c8b0b9.png)
    - From the data the follow hypothesis happened
        1. User accessed Google Mail
        2. Soon after interaction with "file.io" a known hosting provider
        3. Soon after Microsoft Defender SmartScreen initiate a file scan triggered by a file download via Microsoft Edge
        4. See the destination IPs of the hosting provider file.io  
            -We can search additional instances of the IPs  
            _With the verification of the user downloading the file we reach a crossroad._
    
    1. Cross-reference the data with the Threat Intel report to identify overlapping data
    2. Conduct an Incident Response (IR) investigation to trace the events
- We can continue the investigation with the file "invoice.one" obviously being opened by an application OneNote  
    - Use Sysmon event.code:1 (Process creation) and process.command_line:_invoice.one_
- Note the parent process of the event and find additional instances  
    - EX. event.code:1 AND process.parent.name:"ONENOTE.EXE"  
    - Pay attention to the revelant timeline to dismiss events
- Follow the new information and note the query  
    - EX. event.code:1 AND process.parent.command_line:_invoice.bat_  
    - If powrshell is utilized we can find out what processes it created by  
    - EX. Process.pid and process name  
    ![a10e57c5695fd4426e065b08d0712b29.png](35fdcddbf7ab42cd969e17cccf45dc71.png)  
    -Because of the time lapse between activities most likely human interaction rather than scripted unless random sleep occured between actions
- With knowledge of the C2 server the connection can halt so pay attention to the dns.answer.data
- Going further into the investigatiion note the process.hash.sha256 to find additional instances of the attack spread
- Finding password Bruteforcing. Use Windows Event Viewer  
    - (event.code:4624 OR event.code:4625) AND winlog.event_data.LogonType:3 AND source.ip:[8.8.8.8]  
    - EX. event.code:4624 (successful logon )  
    - EX. event.code:4625 (Failed logon)  
    - EX. winlog.event_data.LogonType:3  
    ![0857c6e46021a694431125db0b29dc6b.png](c427e996191343d28b9bed5fb85b105f.png)