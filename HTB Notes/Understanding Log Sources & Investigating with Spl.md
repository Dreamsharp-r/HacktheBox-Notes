   

Understanding Log Sources & Investigating with Splunk

What is Splunk?

- A highly scalable, versatile, robust data analytic software solution know for it's ability to ingest, index, analyze, and visualize massive amount of machine data.

![25335284e3adb681850b741b29a55b25.png](1397656183cd46688993c1dbb751fe67.png)

Splunk Architecture:

- Forwarders: Data collectors that forward the data to the indexers  
    - Univeral Forwarder (UF)  
    - Heavy Forwarder (HF)  
    - HTTP Event Collectors (HECs)
- Indexers: Organizes and stores it
- Search Heads: Analyzers that manipulate the data via Knowledge Objects. Also, provide the interface for users.
- Deployment Server: Manages the configuration for forwarders, distributing apps and updates
- Cluster Master: Coordinates the activities of indexers in a clustered environment, ensuing data replication
- License Master: Manages the licensing details of the Splunk platform

Splunk Frontend

- Splunk Web Interface: Graphical interface
- Search Processing Language (SPL): Query language for Splunk
- Apps and Add-ons: Additional functionalities
- Knowledge Objects: Include fields, tags, event types, lookups, macros, data models, and alerts

Splunk Basic Searching  
![259dbebcf846870e82ab62858b2e6af3.png](a323381746004c26ad4ce870a578d2e5.png)  
Commands  
- EventCode // sysmon event code (in this instance because of source type)  
-fields // exclude certain results  
-sourcetype // Specify the source type  
![504ee50320e7aef8a2230ab3195604f3.png](4bdc8f5e5ec3407b9986c5e1a08080ab.png)  
-table  
![bee79354bff016c6e02c6e4bc7f5c8ec.png](c5fa8536fa694095add030a9777f8eab.png)  
-_time // timestamp of the event  
-host // name of the host where the event occured  
-Image // name of the exe file of the process  
-rename // ![8dcf174f25716b8f47b41d72cc5899cc.png](95ffb70437ac4feb9d61f2e4fae9c836.png)  
-dedup // removes duplicate entries based on the Image field  
![64d5492a63b9afc20650a9aef32699d5.png](675fdafc79ee4ec1bf2111e26be2a064.png)  
-sort // sort all events based on timestamps  
-stats // sort by unique connections to events  
-chart // visualize the data over time  
-eval // creates a new field with the setting indicated  
-rex  
![0f7af42e05a223bd3864a82b789d9293.png](0d3b40afeaa34c9897a229a8a8d3ab65.png)

```
-lookup
	-index="main" sourcetype="WinEventLog:Sysmon" EventCode=1 | rex field=Image "(?P<filename>[^\\\]+)$" | eval filename=lower(filename) | lookup malware_lookup.csv filename OUTPUTNEW is_malware | table filename, is_malware
	![bc95a432efa42d7c9ef31eba991a9bf3.png](../_resources/da06c2d5ba65467894739ec53ba0f95f.png)
	-index="main" sourcetype="WinEventLog:Sysmon" EventCode=1 | eval filename=mvdedup(split(Image, "\\")) | eval filename=mvindex(filename, -1) | eval filename=lower(filename) | lookup malware_lookup.csv filename OUTPUTNEW is_malware | table filename, is_malware | dedup filename, is_malware
	![446bbe8b1e9ce284b53709c0e71e742c.png](../_resources/cd1a069b06e64b35a5614d9c1a997eca.png)
```

- inputlookup  
    ![d893acb155f8b8740b12605bdabbdffc.png](f9043386cc8444308f2b5b50bb05277e.png)
    
- Time range  
    ![bbce9de113c546e19f0840bc775bf929.png](829c8c03bb9745368c2081465c91111a.png)
    
- Transaction  
    - index="main" sourcetype="WinEventLog:Sysmon" (EventCode=1 OR EventCode=3) | transaction Image startswith=eval(EventCode=1) endswith=eval(EventCode=3) maxspan=1m | table Image | dedup Image  
    ![78683a99d7e92cd0e03fefffc28fc47f.png](5fa6f325a69444fd84c98d75d467e635.png)
    
- Subsearches
    
    - A subsearch is a search that is nested inside another search
    - index="main" sourcetype="WinEventLog:Sysmon" EventCode=1 NOT [ search index="main" sourcetype="WinEventLog:Sysmon" EventCode=1 | top limit=100 Image | fields Image ] | table _time, Image, CommandLine, User, ComputerName  
        ![60f80938af89737dfd1963af9834b7e1.png](604af2c67bc54c328df4ca385a1c8ac0.png)

---

Identifying the Available Data

- | eventcount summarize=false index=* | table index  
    ![36f0ad39899d1909c2fad9c465d3f6f4.png](c02ea69148d34607b74c587281e3406e.png)
    
- | metadata type=sourcetypes  
    ![b3add8fb9a99877b30e87eef1718ec96.png](172339bd73504592a9ad93c4a2b58b0c.png)
    
- sourcetype="WinEventLog:Security" | table _raw  
    ![f2277dca681c603cb97e0dfff07ab855.png](5f1bebb251254a57a7d006742ec6b31d.png)
    
- List itemsourcetype="WinEventLog:Security" | table *  
    - List item Can Identify the fields you're interested in and specfiy in table command  
    -fields Account_Name, EventCode | table Account_Name, EventCode
    

![9bb067ef3bdf3ad14cf243bcc1a0caab.png](c0c745d708784e09928f326e4fa3a553.png)

- index=* sourcetype=* | bucket _time span=1d | stats count by _time, index, sourcetype | sort - _time
    
    - List all fields within a specified sourcetype. Make sure time range is large enough to capture all possible fields
- EventCode=4768| top limit=20 Account_Name
    
- Find Account_name and sorts by the # of Kerberos authentication ticket request
    

Searching Effectively  
![06c50d0da97b629f326836943b400fe4.png](4378914d715c415a85a1eb96596f0414.png)  
![aa585684f2e1cf21412233af21580da7.png](00ca10d6507940f98e06d760f35ef15c.png)

- Look at Sysmon Event IDs  
    ![97a17a346ef47a86758777f35b7a9da0.png](28158c035ce64c7396888096a6fdf9c0.png)

---

Crafting SPL searches based on Known TTPs  
![b318e44b63dc67ee1ad83d1a2eb96d97.png](02aa3f00b1234f0e8251eb0846d6a532.png)  
![27b34fd1953f2f5d31d30957c602a650.png](6682382f03f445588da58f302b837a17.png)  
![789e1d4413d9a566bc75bdfa4853acd4.png](a962a7c39ce341ddacf8a3f7415ad529.png)

---

DCSync Attack  
![d059d51436bc9fde6d420b10fa21dcdc.png](f587bc3f733f48a4bc3d1eb9c065221e.png)  
![37d0f122a07644c31e1f4e6737d2d52a.png](2eeb40552b3344f8bf2d5c81e6c64678.png)  
![6a30bfc38981ee487d76ebba03dd89b2.png](713a54b10a844f3483d9be22b4d5bbc5.png)

---

Backtracking an Attack  
![a28ecd3ca2f4c246e5e52ea8543895ce.png](1916835b78954c17adc8c815dd226de9.png)

---

Meaningful Alerts Creation