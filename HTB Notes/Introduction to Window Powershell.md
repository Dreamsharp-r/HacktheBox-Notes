---
tags:
---
   

Introduction to Window Powershell

Cmd vs. Powershell  
![75e54308fb2828f1aaa6338b6949d5a5.png](6c750b6faa7749619f10d32e25d52663.png)

![1ed73736779d15e595b11d8376186b63.png](13f00917f8ef4b22a0cf6601f7a23bc0.png)

Admin Commands  
![b40ece0012dcdbe6e73f12782a000306.png](4a361cf50d8540dda1a288fa9bfb2644.png)

HotKeys  
![d632421d4d083218d4f7c39dd2bac9f9.png](21204545cd994f3da2d0ee68b2fa9de5.png)

- tab // Autocomplete command
- SHIFT + tab // cycle through commands  
    General Commands for both CMD/PS  
    ![b315aa8d45ce5cbec4276be6fb270dee.png](bd01aa9ec52e425886f0f9235512ebdc.png)
- Get-Help useful to find information about a specific cmdlet
    - Aliases are shorter names for commands
    - Update-Help useful to make sure you have the most up-to-date information
- Additional Commands
    - Get-Location // view the current working directory
    - Set-Location // change the current working directory
    - Get-Command -verb [search] // search all commands within the search bound  
        ![028a566146b3f5bc4731410093bc0447.png](3cf8364d7560494ab321473a9d9fdcaa.png)  
        -Clear-Host // cls
    - Set-Alias  
        ![0b68ba564605db8fa411e81b115b93a6.png](7f464d7afc434db8a81fd36ef7275315.png)
    - Get-module // Shows what modules are loaded into ps
    - Get-module -ListAvailable // List available modules
    - Import-module //import a module into ps

---

File & Directory Commands (PS)  
![20e97d2795cefff0991fdb81927b531a.png](aebc12a1e69a40dcbbce832cd56c3523.png)  
![7e0541be32f295a69a0a3ef8c0374b12.png](5a9ed5d3587347dfac8c926c1a687df7.png)

- Additional Commands
    - Select-String (sls) // grep

---

![d2095f7a64c2fd10395e4947a53c33da.png](708a77f07ca84e6bac3555b66fb9ea96.png)

Find & Filter Content (PS)  
![8cba373ca83e3bdc139a41c16eed8247.png](c8812643197b462aa90b08f59b6aca81.png)  
Pipeline Chain Operators  
![131a272898c236bf45b679104cdb2094.png](a9abff004ac8472abaedb01a04d45b95.png)  
Comparison Operators  
![1ba5988fe26333e4f2bc060ffadc1c87.png](985779da20e04525b8197e5e4789cfb0.png)

In Use  
![71c1156f05be31737c255623b5f76f83.png](679a41f4783148f68b927866044c2130.png)  
Filter Out every service associated w/ Defender and display all properties  
![9b7004d98e2690f345fc6c49e1adce71.png](9bf590c49c8d4607a30a3f915cc83bc3.png)

Examples:  
Property Output (All)  
![adb69b389e3c087e27bb22467c713908.png](6f3a433e60e64e3fab148ba7433d54e4.png)

Filtering on Properties  
![bbeb69eabba1add19bdfbd0f8a13f635.png](1e0fc6d763af456c96d051710668f462.png)

Sorting & Grouping  
![1bdb11cb6b5cf125be2e78318e41cb85.png](dce9f1e8a33e428a9f93abf5af2c741e.png)

Too much output vs Sorted  
![2e593b67d08c5020a5930431d74156e5.png](dcf547743a584b36b81e98ef8b28e839.png)  
![5bbf67bc40f4f456b2371cdba2460b40.png](09c329a0f0f74db2a85f9fc2d70033f9.png)

Finding files within a directory  
![120326012355531e8bab917e63579dd6.png](217286760b014ad9893c7c0f46b69809.png)  
![e08b0cad4a153c1031b102b3cd9e8466.png](2af15de7eb684f3f8bcd64da80a04ae9.png)  
![adcb64fb02ded0f205c8407c73a29c78.png](13351ee27086468fb3a5ee3670f553da.png)

Modifying with an "OR" statement  
![352e40626e8c7490843ce78cf19a7603.png](568cc4dde743429689d1e05c9625f0db.png)

---

Execution Policy

- In order to run scripts the execution policy must be configured  
    ![6d2463aea9df97d3f92f0efcd42e2c37.png](ffc75f13fa3243a7a11e17a3d996321e.png)
    
- What types of information can we gather once in the system?
    

Breakdown of the information gathered  
![d959782fe0f4ab05fdfab70bc7e42c92.png](c90e3581441d4978b2889322ca3443ae.png)

Example of a task  
![6f6fef7c885a4a5f712b29d54c858a31.png](ba87b0ed483d4df980fdf925e5b7a0ea.png)

![a90f844de1d12a2b7e0f610dc38c4627.png](f3e7c67024664f1d83a8766af09baa27.png)

How Do We get this information?

User Commands (PS)  
![f7a21e272b00186d30d69a048f37786f.png](9d9cca6447a043189aaeb136426ec48d.png)  
![59a6334af38ff617a79314e1a137cde4.png](76df1218a3194488957f57e2e76679e2.png)

- Additional commands
    - get-member //shows the properties and methods of an object
    

Network Commands (PS)  
![92568eecfcdf47baec6dc6c7e1af96a5.png](7cf502f6ea0c49d29d619283dc2cbeaa.png)  
![539672899981d06d704830f3b3c9b012.png](09b6d7c7cffe47bea2a83bcf63c3665d.png)

![32bb24594000bd06b5c19c7939b14e2e.png](bf652b87bed44d2984da678519f14bd3.png)

Net Cmdlets  
![ffbae3986f4b80d74e44e97fe6b8ba7c.png](4a44db75d83c4f249b9099a94640cd85.png)

---

Service Commands (PS)  
![a53d094bdbc3cea821028477785fd3da.png](8eb5e92d8568419da520a53f34a72581.png)

Examples:  
![769e2d19464f3eac157bda4e882e3ac5.png](c1c7ffae35954a97b7d8d2f07070cd3b.png)

- Add ft -Property Displayname, Status

Filtering for a specific service  
![460c96b1fff593cb9c769677c34a6cb9.png](f233060f0d2d42ea90b06071cb5ee0a7.png)

Remotely Querying for Services  
![fd2314719f83729eed43afe4a0e87865.png](6ddb6a46dccd435ab4ca00aea84e287c.png)

Filtering the Output  
![b4669a06fdd9d8c88e141808cdf43aa8.png](9b5d7a8b66ac432986d14a4fb118fab9.png)

Running a command on a Remote Host  
![a22fd690b73e82bd697c16d3c9fad13d.png](1faefa4c083f485b80410f5ca9a1993a.png)

Interacting With The Web  
![4941e23f668a027c765b50acc492cdae.png](ccea3b47c0854f39ae6a6a0340b6545d.png)

Making a Request  
![90c00968657e4a0b817d406f857bd738.png](663cfeda74de42a78045e534685b3a4d.png)  
![1d01021382e17d76a40d3f32521b4a93.png](b3c03aae13234fbab0208a29d27a06fe.png)

- Get-Member shows all the possible content on the site

Raw Content  
![fe8e260917937feb51dc2e9d18c8dfec.png](f2ba6cfa34b84d00935ca588bafc292b.png)

Downloading Files via PS  
![65317d6b225b4ee1c89f5effcd8e71ea.png](ba46889b5abb4aa2802260926b87861a.png)  
![8d9a50695a516223b8447510f6b34136.png](bbccffa0a94c467d820ecd43e88a86a5.png)

Downloading Files via .NET  
![fcdfdc041d637f37cfa6353354057d41.png](ccf31c6fb27b4ceea0bca8e200fac6b9.png)  
![bae7d5b2ea65ce692ab62df7d2b321c5.png](2af1a5acf7b84af094c0a9391639ef7b.png)

Event Log  
![31fc018a9112424576a369559d61392b.png](4112e3b57881465cbf1a8e4f83e5c8c2.png)  
![0f533db3c46be71b4e051a4a776b62fd.png](3b44fca64f2a4f5881223aaeeacd8444.png)

Event Types  
![bfb67e5088d0c68f5e8effaa77dc52db.png](84741288b5004c8d9b60230f27669dd2.png)

Event Severity Levels  
![8b3fd59dff3cc745ab0a3f94da51ecea.png](11413fecd744462da1c0c5df5c699565.png)

Technical Details  
![ca346460770bf733f7e0243540c8a9fe.png](8d19522fca5d46b890b3993f1abc5237.png)

How to Use (CMD)  
![1ffffb58c5bc81bafc750ebd1c3bce6a.png](de996981999247d8b05a1ec8ec71f21b.png)

How to Use (PS)  
![935bfdbfc33fd02caae69ae170a196a8.png](dc8cbb47d68b4228a814580562a82e9f.png)

![186d08bde6affb97d93afa3cad88ac31.png](6b2e58141e3d4cf2bff1f40c90e0e94b.png)

Filtering for Logon Failures  
![90abc784da6cf79c990df032672f8d6a.png](ede3774d0d5b4e1f9c54835a3a3acc76.png)

Filtering for Critical Events  
![fd51a7c33afe1ea6c534082f59e9e716.png](197ab753a4764caebec48e52fe057d09.png)

---

![7e26c8b2f523500c2f2a4a7926bfe2f9.png](3d9b4fe83e0e4bc780d8e1d52f79b120.png)

- Registry composed of Key:Values pairs  
    ![ff79a1c15339347c40b979c239f59949.png](7c903c29db714f46afaff1e092f7ab93.png)  
    ![01b64ac22b20c07f15042156b16cdd92.png](426076fffd8142d28c23d3bab2bd7303.png)  
    Registry Commands  
    ![214bd3e7f90de94930d7603e7c32f698.png](f3aac321b35a440198448d0cc3412fcc.png)  
    ![ea0b7b833ab222549e3f7e54627322c3.png](d28d43a6e2684fd094bbe9b3d22858d9.png)

Examples:  
Root Registry Keys  
![7c2f6ffb7e6a9839d389c19425d999b4.png](0d9de6772a8449b5b966051cd4be156d.png)

Recursive Search  
![630cdeede5a15022044721fb2238cac1.png](b273c8d1f34d433792e5a8b079e86bcb.png)

Creating & Modifying a Registry Key and Value  
![9ff935339bc29b9c04033c3593d29ae1.png](1bd58eefecdf4c5f89f2d0c0f43a86a0.png)

- -Path parameter allows us to add a key to the registry w/o changing location in the shell

![ee31c60241991242ec1587966e580bfe.png](6ee1049d3a8840de84ddc24d90c02698.png)  
![b401847df1c6b143ba7f234e88061118.png](21ebe03e3a7941289bead507d2f06397.png)

Reg.exe code  
`reg add "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce\TestKey" /v access /t REG_SZ /d "C:\Users\htb-student\Downloads\payload.exe"`

Powershell Scripting  
![6f722c4489fe1bdd1057cb9fbfa6f94d.png](8896c070b19d47a1a2c17bee83b25660.png)

Making a Script

1. Make a directory to house the script and dependencies
2. Create a module  
    ![96221ca69dde753791dbbee50c01bcbd.png](2165812c0f6649698d09bceec751be4a.png)  
    ![d7335dc6e0fbac3453ec1dbd3e7de3ec.png](e320e8746d6b42d9adf31956dd8da175.png)  
    ![6e7d4ecb87cbdcae5de6f40ad5fa03ed.png](043dcd76cb65457e875b00e917ec3ba4.png)
3. Sample Manifest  
    [Recording 2023-12-29 140549.mp4](../_resources/612d5fc04362466c90cb9b0edbe099c9.mp4 "../_resources/612d5fc04362466c90cb9b0edbe099c9.mp4")
4. Create the script Ffile  
    ![16795d5c83d891086f3363da42de4b88.png](9c3fbe25ed5b40318dcb725498c25523.png)
5. Importing Modules you need (OPTIONAL)  
    ![13f286f3c0d1df7edb81ac694becbb3c.png](1536c62fc0794b7d8bae8419a03f53fa.png)
6. Writing in the Script  
    ![bc42971f5778559efab3217ceeb17b3d.png](e96d9c4acf704f1b85411deb0440b408.png)  
    [Recording 2023-12-29 141843.mp4](../_resources/70d669a6239f48edb6afe8b6f8a043f5.mp4 "../_resources/70d669a6239f48edb6afe8b6f8a043f5.mp4")
7. Adding in Comments to the Script to help understand  
    ![adc1f4d88aefdf0109cca31f03dd19de.png](79d13addccd54a1fb3146d6d819f2744.png)  
    ![4e4b7fc3bf8d620b2d02702ae8707904.png](8721d3e3d8944b1091e748fb1eeab100.png)
8. Final Product  
    [Recording 2023-12-29 143724.mp4](../_resources/47286c88311b4aa5a8b530f63f8d4126.mp4 "../_resources/47286c88311b4aa5a8b530f63f8d4126.mp4")
9. Importing the module  
    ![b179ebbc9746623a6d2ab1b96b65790a.png](40ef3941464441ac8fdb2ca8f0dfdfe3.png)