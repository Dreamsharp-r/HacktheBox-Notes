   

Getting Started

Basic Tools

**General Tools**  
![5e0b8025e61998e1cc7dc37d07906e7d.png](7ea9667550514dcda62265caf36b4e1f.png)

![7cdb6d27102c9e9bc9ef737e966094b5.png](2e3d01c2d24544858ec3365e2d5064fd.png)  
Two main types of VPNs:

1. Client-based VPN - Requires software to directly connect to the company network
2. SSL VPN - Uses the web browser as the VPN client. No specialized software download

**Types of Shells**  
![f2568d38bd8cb7f5ae1d305c83b6a42b.png](568c9ad4f6c941848459e3a21bb20e34.png)

![d55be0510b945b839e04816a5ac74030.png](68bffc50991c4762b56ad1d4052c37c6.png)

**tmux**  
![3e5045b4124c4acb96ed6115d8eebabf.png](e8b1273d354748d8b2c0d28e3dc673ba.png)  
**VIM**  
![193eee56d5aba248e974fbfcf30c4309.png](76b42844473640878ebf715b16cd6235.png)

- Pressing : to go into command mode.

**Pentesting**  
![87401ee3b6b71ae4fd276fb3321a6de7.png](eda4e9d1e6e34b00838993ae8cfc73c7.png)

- Netcat allows you to interact witht ports.  
    ![b131d1005e78fc1b4d40d7b334d9efd0.png](827317053e4c4f869a4098ecde3cfaa3.png)
- Allows us to do **Banner grabbing** to identify what is running on a particular port
- Can specify specific scripts to audit a particular vulnerability.  
    ![d380772aa0c02a1c809f51e730d40077.png](e20e2bc8505c4211b5f3b2ab48a0dc3a.png)

**Web enumeration**  
![6fbc4f1fb351e585cc859ab60ad175bb.png](af81a5a96a444cb09176dec2746e39f0.png)  
**Public exploits**  
![6b63b981cfc473114e7d229b60d39cfc.png](b20aa3452e514b52a761b098d0bb70c3.png)

1. Use searchsploit to find vulnerability or manually search
2. Once found activate metasploit
3. Match exploit found to one found in metasploit
4. show options to set parameters

**Using shells**  
![c91e05513db19d896401c5fe996936d0.png](0e7756a834224de9a35bde14fe105914.png)

![ec96fd52291d507c3d2c9334e097801e.png](ceac196e25b44b049b0daed995884a6a.png)  
Default webroots over common web servers  
![bade1da1f5147db40e6b1fad3c4ee089.png](29e8a20a03584d69b8848c6c1a6a1a26.png)

---

**Privilege escalation**  
![989831ef625054d829390f3094075441.png](f9d8134e3e9a465aa1102398e91cf68a.png)

- Appending to the test.sh via "/bin/bash -i" because its a bash file the cmd will get executed as root. In turn will open a root shell  
    ![85fae37219318c9715a0916eb9f88f25.png](4a3325b06c71419c9f5b848280c8eef7.png)

Privilige escalation using nano  
![1881a1b47ba3f1a9231d2963ae362ad9.png](1ab73f5d92334a618847937e18c81287.png)

- run the command sudo nano /var/opt/../../etc/sudoers  
    to reach the root file. this allows the traversal of directories while utilizing the allow root of /bin/nano.  
    -sudoers file can be edited to give root access to a specific user

---

![2e1dbcfcfcc4d3b3e5084ba50db270f8.png](7a025873c1a04d53ac6e0452f0150bb8.png)

- With vim you can open a shell within vim
- Switch to the cmd shell and enter :!bash

![223725bd5c196da437057024f05665d5.png](ea8db698348447b8aa809d6ce8f405ed.png)

- Run the first command in the shell. Output should be the same.
    - sets the environment variable “CMD” to “/bin/sh,” which is the path to the shell interpreter
- Run second command.
    - The `sudo php -r “system(‘$CMD’);”` command executes PHP code with root privileges using `sudo`. The PHP code executed is `system(‘$CMD’);`, which employs the `system()` function to run the command specified in the “CMD” variable
    - Since “CMD” is set to “/bin/sh,” the PHP command effectively becomes: sudo /usr/bin/php -r “system(‘/bin/sh’);”

**Transfering files**  
![b03ca548495d22b4afcee3d0bff557d3.png](0a1a8d687ea546a4911dd119de76792b.png)

- To transfer a file you can start up a remote server