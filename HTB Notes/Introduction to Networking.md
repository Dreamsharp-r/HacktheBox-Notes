   

Introduction to Networking

Big Picture Network Map  
![22da6241222b4f293fc542970f504c81.png](c407ffd237f54efeb9dc98a4a6a0dd51.png)

OSI Model  
![7cfd4fe86cffb65bca3d524f0d9658a9.png](f309c39b46574d4a8fb20bc31f488aa8.png)  
![b346ca9898e14769cf75ed667ff3af7a.png](57606bc10b3f476f968a87e38bdbe40a.png)

FQDN and URL differences  
![cd72757659b7e05a4c51e10b51235dab.png](48d9515dd2e24aa79f9e014fe7269070.png)

Tree Topology  
![4cbbe927ef416d39843ce2d39f965a40.png](436475308d60465d9742ae2fa6f5e241.png)

Mesh Topology  
![ced618419ce8534c808b89cb95f58fce.png](beb001ffa6b9416d8f14f015257cfb2c.png)

Forward Proxy  
![476f54ac6065a3240a7c7e245eb342d8.png](b6f5e82bb09b46b9876b1c7e873cf871.png)

Reverse Proxy  
![454627f039c45b6052d38f11b04c1c00.png](a71666c5c49240d98c89508c2253066a.png)

VLAN example of segmenting a network

![2ca0f2a42a5b73ed6a01ac4a66280da9.png](551479537bf9456f890a04e48031e8af.png)

![4f8f1af5e2bd21571166f247c4c79abe.png](c692363ea89946a0bf033af5b520a9d6.png)

- Two main trunking methods used, ISL and IEEE 802.1Q
    - ![23cd7f77d0726c4e0d2d093d75de084e.png](b00356a0e2ab4c76b95d939c1bb98273.png)

Assigning NICs a VLAN in Linux  
![b788bcec37a50ae7c5452313228ee658.png](be436644bbf64a13aad36dbbd97f8f09.png)  
![8565fa331a6b8d806653b6a77124e737.png](b2c8b0a292d040778830e895c68984b7.png)  
![faa5577550de6b6499a340d745671d48.png](742b1cb450a34c7084680c7593ab0ed7.png)  
![dc6eb632308512e9dcd0264baec816ac.png](5160bcd4d8ab4746920cb9c8d921b76e.png)  
![293dd14eb14e2de949408c1c94634fba.png](999ef50bc3cf4f44ae1e0e069b697b76.png)

Assigning NICS a VLAN in Windows  
![0ee995fdd767f945f3bbf2a1e9fc2ab2.png](837463542179472f908767b432888e40.png)  
![cf90d3adfbd28ebeb7ba619dafe87ee9.png](08d945eabc2643e5bd7968f0b2175e87.png)  
![5398ee8fbdb50515d26d00b5196f56ef.png](12ddf60e69eb49c7933c9c69dcf1d311.png)

![f1d8a1b0d1bdad0f8caa7c5a4fbc1f97.png](44d1365f625640b88d4d82bbbfe309ea.png)  
![b6ae6770e20c061bc2d007b9aa066d59.png](8688d7aa08ee4ec89cdf7a7708112e72.png)  
![b9bee58b7f643569ce340df76846c88d.png](290cbc33dcfe4642b2d5198eb77d7f05.png)

Analyzing the VLAN traffic utilizing Wireshark  
![ccbeaa86e83d820dd9a785849cd312c0.png](106393dc335c4a7da6d20632ccbac503.png)  
![fdf9af4ba212d82654ecf4af48acc827.png](4f5afefc1d304e5aa916ae300254f409.png)

Analyzing VLAN traffic utilizing Tshark  
![6dc1bcedb84bcac7a4d39c3b4342b8d2.png](ca9808a9159e40019a544962277d107e.png)

Types of VLAN attacks

- VLAN hopping - enables traffic from one VLAN to be seen by another VLAN w/o the aid of a router
    
    - Exploits Cisco Dynamic Trunking Protocol (DTP)  
        ![f4229f568171065fbc212b9b2e92e1d4.png](a6af6552911d4661b3c0fa4abc0f3046.png)
- Double-tagging VLAN Hopping -traffic that already has an 802.1Q tag are embedded with a hidden 802.1Q tag inside the Ethernet frame allowing the frame to go to a different VLAN  
    ![1890ef07e7d4bad8352263c0ada7f65e.png](c68fca48ccdc44bf94a3e3fa1bd70da4.png)  
    ![66ccc8212a7cdd0296be8cd6e50de80e.png](9604099e80604c6b99b869968364cf5a.png)
    

1. The VID field w/n the '802.1Q' header only support up to 4094 VLANs
2. To combat this, VLANs which operate on layer 3, the IEEE 802.1D Spanning Tree Protocol (STP) was built
3. However, STP, has its limitation and can hinder efficiency by deactivating links
4. Solutiion is Virtual eXtensible Local Area Network (VXLAN) an Layer 2 overlay scheme on a Layer 3 network

Different encryption algorithms  
![f52d9dbe4a58dae1fa661e47a993c7d2.png](92abf6e7501d4c85b16f03ea07339c52.png)