   

Intermediate Network Traffic Analysis

Fenix5@htb[/htb]$ wget -O file.zip 'https://academy.hackthebox.com/storage/resources/pcap_files.zip' && mkdir tempdir && unzip file.zip -d tempdir && mkdir -p pcaps && mv tempdir/Intermediate_Network_Traffic_Analysis/* pcaps/ && rm -r tempdir file.zip

```
Fenix5@htb[/htb]$ wget -O file.zip 'https://academy.hackthebox.com/storage/resources/pcap_files.zip' && mkdir tempdir && unzip file.zip -d tempdir && mkdir -p pcaps && mv tempdir/Intermediate_Network_Traffic_Analysis/* pcaps/ && rm -r tempdir file.zip
```

How ARP operates:  
![788a4c8bfbd1110a211403ca2265698a.png](2b5d247881864d04b27ac4655c439ce3.png)

How Spoofing works:  
![9e53f8a6782653ca14c996b85537ba8c.png](1a9e2051ed77447fb1c43a8f5d025a53.png)

How to Prevent them:  
![efe5040b4072b4249a32bdad0e3476f7.png](0e7dae24074841cc9f758dac757e72dc.png)

Investigating:

1. Focus on ARP request and replies
2. Filter and examine data detecting multiple MAC for a single IP
3. Validate on the system by:  
    ![c7dd20498cd05211d248ea4227c7339e.png](8d1f6afce32f48e2980f9f84eeb92fc8.png)
4. (arp.opcode) && ((eth.src == Source MAC)) || (eth.dst ==DST MAC)) // filter to find the IP change
5. ![1ecfcc9fada2bb96c18713ce826ba72d.png](0e329c7eb9d24b0591819ea3572a5d15.png)

ARP scanning signs:  
![2af0fe22418b7a4c4e630b1df00c3b81.png](01fad02af5b1494b84a8ab160697d58f.png)

DOS signs:

- Duplicate allocations of IP addresses to client devices and new MAC for all live IPs.  
    ![880bdca5a983751f6b91833e1a96a464.png](f2493bfd26be47298290df52134825e2.png)

ARP commands:  
arp.opcode // Focuses on ARP requests and replies  
- opcode == 1 // Represents all types of ARP requests  
-opcode == 2 // Represents all types of ARP replies  
-arp.duplicate-address-detected && arp.opcode == 2 // Sift through duplicate records

802.11 Denial of Service  
![df42a985c82f62f6e338165e696ed57d.png](2322bff3c6c548f6aefb483993af3f7c.png)  
![c65406c70981e76fd523c57fbdb21f39.png](4ccb5ee4c0cf4d099d964a85bf63ba1f.png)

Restarting in Monitor mode  
![713e995539a1ee19c515a9098905464a.png](cc71d156ea974073ade4fa1b823de378.png)

- Monitor mode same as Promiscous mode
- setting airodump-ng will allow you to see all traffic traversing the connection  
    ![9c71f5adaaf64cfc0180a0497f9195b7.png](5281479d2a9640b9a3a93cebf20b6815.png)

How DOS works:  
![a758432e1af4420a50d7fc5da0731080.png](790ccfe3e7a9410a81f7ce6a9501583e.png)

- DOS alters the MAC of the frame sender
- aireplay-ng and mdk4 use reason code 7 for deauthentication**

How to find DOS attacks w/n Wireshark  
![0672cc1de01b0e50c5a76410e9711c4d.png](52a485c93ada4652ae9d70c4fef22a88.png)  
![48045227bfb44c9cd92cb4ba9a5c4bc7.png](407668fe15b344fcb02c0957eb5c207b.png)  
![549233843908b4bcd0e3da8e026bd7b9.png](9dae5c3d2417496eb05bcc1b8c4888c9.png)  
![87a424d2483f253cf118e0c246b59135.png](6cb72ec4f6ab421c93c2ac6f130ecf12.png)

Tricky DOS attacks to Detect  
![8bc1bc4b9c6feaec56cd2c1ddad41a01.png](54a75ac4481a4026b526ccf97fc59668.png)

- Shift the reason code by 1

How to Stop DOS attacks:  
![728d297945c3885d39785bed70a859e5.png](9bb2439c71604175925db1e5d5e9c388.png)  
![9d4132e03405dfd4dc91502d945fe07f.png](2723083426be4acba4b61e718ba14e9b.png)

Wlan codes  
![c0b576af0ec3a3b3d01a15caddebe3ea.png](1e98fc0a838646dda0f6e0cd5fe2e290.png)

Rogue Access Points

- An access point installed on a network without the network owner's permission

Evil twin

- Is an exact copy of the legitimate access point within the network

Finding an Evil twin  
![2bfff51fa9684215f6e099e9537f8cd6.png](09c9a202b0214fdf9012c7378fb4c7b0.png)  
![015cfb96210702c6bcf91f22365f3a1e.png](147d204aa6a54b319ddb228d1e0cf37e.png)

Finding the victims  
![1be82d873e0c75e764a7ec7c1624cf3e.png](f90755d1349f45d0a8e1c17ec0b62581.png)

- Filter for the evil twin mac address

Fragmentation Attacks (NMAP)  
![101c669082baa168d7e1c5db63c483f1.png](087c177db3ae489e80367fa2cf8588dc.png)  
![bd929c33a8c887d8c9f90f700d405be6.png](af597bc7eeb543558c67e1da12a4c413.png)

- Indictive of a nmap attack
- tcp.flags.reset == 1 // shows all reset flags

Prevention:  
![f1d6d0c2177168a7fce588f8feea1fab.png](e0f0f2f1e30546d680409d5a92a91550.png)

IP Source & Desination Spoofing Attacks  
![d10d6674e90b208ed607961fccc632a6.png](ccc2e1fc4b814fafb77f68bcfedbabb7.png)  
![b8704e8115bbf8b1beb8005f131cd62e.png](9a8c0b134353422a8bad099f29b641d1.png)  
![5b2c358d885b0c90917c51f515ce1a9d.png](3549434898d54736be32a88f4c49b0d9.png)

ICMP Tunneling

- Recognize by the size of the packet if over 48 bytes its potentially tunneling data via encrypted text

Flags & Recognizing Abnormalities  
![19c7b194188461d57a542318bdbf1e3d.png](9291c5f7d47443639a86a6fd481dbcf6.png)

![2104c20c2f14a3c084a4014b5c44b155.png](2a40118f76f34da5becd2150fbff3868.png)

HTTP/HTTPs Service Enumeration (Fuzzing)  
![bd411f9ce2f2de3cc697ad1bc58ec152.png](c542aedc5a144042adc3edb28091f46e.png)  
![4ff7faa652113a587212ab39fd92d967.png](dbee54ae231b4366a6abafebc0516c76.png)

How to find traffic w/n a Web server access logs  
![be58a89e3d815b75210f2251da8f76f7.png](eb720a0ed9dd4d58ae23d823165f7af0.png)  
![7ca1ec79e873052ce828774055517883.png](c7ae0f6438704ceda1a400e5215d76e3.png)

Strange HTTP Headers

- Weird Hosts (host: )
- Unusual HTTP verbs
- Changed User Agents

Finding Strange Host Headers

- http command
- http.request and (!(http.host == "real host")) // Search for all http.request excluding your real host ip  
    ![fbb41513daef1f9407f9f41f069f08a0.png](cc34ea04a62b4d22aeb2ef23153df84c.png)

Prevention

- Ensure that our web server is up to date
- Ensure its configured correctly to prevent this form of access

Unusual HTTP verbs

- Code 400 indicate a bad request from the client  
    ![19e554be45d3529b61e3e017212fc851.png](c5ec70cd792c4cc98a62c2899c2f62ef.png)  
    ![baf749f5bb08af7e0e6cefac55aa4a26.png](b76d09bce4814d2c8d6b6ec20b6f07a0.png)  
    ![001499a9ef54c7d654179e5a31dede13.png](a88675572c514412a95e8dfb8f344281.png)

Cross-site Scripting (XSS) & Code Injection

- XSS works by injecting malicious JS into a fronst side web page via user input. When other users visit the web server their browser will execute the code

![8dc2d34b859cdd93d4a155936a7c731e.png](5179e2012a354cb286c1ca2fb0ab8076.png)  
![f02ac4eb3948bdd2a792d3efd642511f.png](4b58bf790f0149bb9eb3c644f6c4d213.png)

XSS vs SQL  
XSS uses php or JS and injects scripts into webpage  
SQL uses SQL and inputs queries to the web server to divulge information, change it, or delete it

SSL Renegotation Attacks

How HTTPs operates:  
![0e3e7b7bf674b43202da5f8ea7cf734b.png](60550284a34445f0a9600c3eaadc72ab.png)  
![5974a581a0c870622f7fc831c7e8e68e.png](5cf12bcc96da418aa477b229adbeebbd.png)

Finding SSL Renegotation Attacks

- Irregulaarities in handshakes that attempts to trigger renegotaation and hopefully get a lower cipher suite
- ssl.record.content_type == 22 // observe the handshake protocol of see the clients hello  
    ![90766b0fd008b675c6a211f78341616e.png](1eb1351f3e714f7ab7384e74b6866dab.png)  
    ![3207c86256af94019449583ea89d0050.png](de9080b270e24db283bcf0ab00a1d971.png)

Why?  
![e39997b26b07a096d902d8e9b98f2b8b.png](550d10017de547e98d95a3bfc8f64def.png)

Understanding DNS  
![d005e4bc517549ec0233d9f94adf2ad6.png](f3e07094821e45009332a3adf837ff12.png)

- Once the local DNS does not know the address/IP then

![21edb2c7e9ca16f224f873601df39429.png](fd70b765a7f6481b8fe2e22b4ade36ef.png)

DNS Reverse Lookups  
![53b830101c3d242a915fa1d58d7bcbfc.png](4e77d0b840ba4d20ae1bf22f2c069df8.png)  
![01195460dda0a902f72180f84b920a97.png](466a5fbd5d4a4ce6ba76d7c970f30189.png)

Finding DNS Enumeration Attempts  
![41e772f441d0934a4719eddf9fc1db03.png](136d28cc7b2c40b1be9a1b9703da3e63.png)

Finding DNS Tunneling

- Noticing a large amount of text records from one host and paying attention to the TXT field within the data  
    ![f2100eafd46385c26c6a8ab8e6e88c56.png](3554fe5d325c4164b1d913cb347fa551.png)  
    ![96dae8d06ff6c42dcbae9998edde48dc.png](d9cfcf9046214f0089d4b786a920394d.png)  
    ![716f5309b4a8a4c73127c71f6eeefb3b.png](a9e612c7621e4377b9197d25033b408f.png)

Why?  
![9f55073b763f2b01b9e829e511da8d2c.png](7c6c992ae18b4e29b7042e2b37003d19.png)

IMPORTANT  
![31b0a60adb3373fd5ef7af600173f4c7.png](a88d124abd0f4669a29696cb3f504301.png)

- IPFS is a distributed file storage protocol that allows PCs all over the globe to store and retrieve files as part of a giant peer-to-peer network
- Anyone can download the IPFS software and host files

Telnet  
Provide bidirectional interactive comms sessions between two devices over a network.

- Still utilized today on Windows NT
- Observing IPv6 traffic w/n your network when its NOT configured for it is an indicator of malicious activity  
    ![49492489ec5af8a15dfc168f2cedf97f.png](26dacd2fe9034843af6f49aacf314c8a.png)
- ((ipv6.src_host == Malicious ipv6) or (ipv6.dst_host == Same one) and telnet

UDP  
-Easy to follow the traffic  
Common uses of UDP  
![29407d8b5dce166d228d5bf6cecd8176.png](8004a8fc7a174e15a30a6ba677f11d28.png)