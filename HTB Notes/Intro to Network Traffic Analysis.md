   

Intro to Network Traffic Analysis

Common Traffic Analysis Tools:  
![32042754a63a98c326423ea4d1418209.png](19b33e7f21f8493e844347c50d0eb0e9.png)

- Windump is tcpdump equivalent

![b92f3ecf29d9826a5f75198b6020ed90.png](cd46e02782344bfaa1ee6069c2185ac6.png)

- All People Seem To Need Data Processing

![a76d401c80faa52ca5fc2d481f657d39.png](f861ba6ffb394c81a8579951ff63c9d1.png)  
![266046ad0f6a198fb66632c437c8a325.png](1c1bbe57c688478da506fecc1edebc3c.png)

![b2023ad28ec830dd2caae7063bdcd186.png](c34576a63f724e6099bba7cf402d12ae.png)

![d7344adcb3111332dd5764b2c71cde4d.png](e9043cb1bead42d5902aeb24c8adcb1a.png)

FTP  
![132158b9fe24b5d107f610e39e4d8273.png](bf5a9e964d2343db92585b75b7cd6c2a.png)  
![9bd759cebd72471622b6334d8c28961e.png](ba4b9f2440604b5288329370494ea448.png)

SMB  
![bc58ad16e8b01aaa9963f9e73735667c.png](ac75912afefd447daf7ac633fb407fc8.png)  
![a03376eaea6099b9ded4ac5517fe6798.png](7f8c55c3beab45c88987476cec71616a.png)

Traffic Capture Dependencies  
![d575bda9d84e243fb90ee8da2046b7aa.png](c1cf0522164849949d56146417387b12.png)  
![24b4bc2d536b0817f9d05844d8eb60e4.png](0e59d43ee6474de081d7ece0a7ef3e14.png)

Analysis in Practice

- Descriptive Analysis
- Diagnostic Analysis
- Predictive Analysis
- Prescriptive Analysis

![9279fceca3d0777d3437b03f82e7132c.png](90eb8ae1181145428878caeb1047b53e.png)

![7fa5594b047678b2d09b3e6ff07ad2b6.png](2bf8637c74b24cac9714afef39d4fa73.png)

![093716260a96f383216d50fbb937820f.png](05ffce6c95d04528a2713bcba3e9c672.png)

![15c1506e6c7db87b230a6b12ffe285d2.png](1fe9f43f73d84bf3948f41757d544386.png)  
![447a9095efd08eb54c9ca5e22b1ca1ec.png](7deeecc946554e4fa922efb5a5d97e6d.png)

Key Components of an Effective Analysis

- Know your environment
- Placement is key for capturing traffic
- Persistence at the task at hand

Analysis Approach

- Start w/ standard protocols first
- Next, look at specific protocols to the organization
- Look at patterns 172.16.146.1/2
- Check for anything host to host
- Look for unique events
- Dont be afraid to ask for help

Tcpdump Fundamentals  
![c4f24c9bbb6ce49008e64fdad1918524.png](51bd9c44065340e5a4f28af3f0c04792.png)

- promiscuous mode allows a network device to see and capture packets sourcing from or destined for any device in the local area network, not just the packets destined for us.

---

Tcpdump breakdown  
![6d1a15eb4690da19271d3003ada8bfc7.png](f2b799a539984c3da247c5f4af377b28.png)

---

![4792772bc495c271586de30d77525002.png](008ca186892441f5bb3a0303400d3702.png)  
![6a7fdbee928fc92890a32e20be2f4279.png](74d914992590451caeef09e7efc8bafe.png)  
Additional commands:  
![3f06d1997bf9c0b8f3b90764beea6dec.png](f29790bd42c34db78a6d73c8c799375b.png)

T-Shark (Wireshark Cmd line equal)  
![7d7eb5b893050d9cd4f6c9434a9adc4a.png](aedbab4dda1146c4b1df35271dc72b0e.png)

WireShark  
![b002fc156ec6217df42821d5dbe749dd.png](a02edc778eec4754b3d772ad82e97f98.png)  
![f17a82e5390697a3ae840f13697c03ea.png](1c25c97163524d5e9366f94de7bab289.png)

- Termshark // cli version of wireshark within the terminal window
- [https://github.com/gcla/termshark/releases](https://github.com/gcla/termshark/releases "https://github.com/gcla/termshark/releases")