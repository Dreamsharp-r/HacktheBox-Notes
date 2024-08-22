   

Introduction

Penetration Testing Stages & Situations

- Internal pentest
    - Provided w/ internal host from which we can work
        - If having internet access can use a Virtual Private Server (VPS) to download the related pen testing resources  
            -If remote then ship a device w/ distro pre-installed or provide a custom VM that will call back to our infrastructure via OpenVPN

Sample Environment Structure  
![64a235cbd11b097c20777437eeb62fcb.png](dba587c7af754a2ba49484d25e5c72f6.png)

Specialized Environment Structure  
![032edbf7156cf13a5877e3e50d29dec8.png](de687c01a0f144beb6094038a5b2fd33.png)

- Firefox offers add-on and bookmark synchronization after crreating and using a Firefox account.
    - DO NOT sotre potentially sensitive information or private resources
    - If you must edit a bookmark list then create a separate account

-1Passord - password manager -  
![7ad09d42dc931289aa4f68f651f23de6.png](676cfa493b1a4d12ac42f222e229e886.png)

Notetaking

Xmind: Visualizing the overall components  
![65575e99c5e381caa1d94492c3f83039.png](c3072d897d91435dbedb9dd997c02782.png)

Obsidian: Creating a thorough tasklist  
![30d47706150b515cde7fbe97e9792a94.png](2b694eb823f84778a68509655ba076ea.png)

GhostWriter: Notetaking throughout the engagement  
![0465dcf810034be9b322869bfa083566.png](bd0000a27572473884475ea7fce2520d.png)

Pwndoc: Notetaking throughout the engagement  
![76e8924ae23b89dadb4582e46f00d7aa.png](99638f585d744977bf2f27be251533a7.png)

Script for logging

- Replace the PS1 variable in the bashrc. file with the following content:  
    `PS1="\[\033[1;32m\]\342\224\200\$([[ \$(/opt/vpnbash.sh) == *\"10.\"* ]] && echo \"[\[\033[1;34m\]\$(/opt/vpnserver.sh)\[\033[1;32m\]]\342\224\200[\[\033[1;37m\]\$(/opt/vpnbash.sh)\[\033[1;32m\]]\342\224\200\")[\[\033[1;37m\]\u\[\033[01;32m\]@\[\033[01;34m\]\h\[\033[1;32m\]]\342\224\200[\[\033[1;37m\]\w\[\033[1;32m\]]\n\[\033[1;32m\]\342\224\224\342\224\200\342\224\200\342\225\274 [\[\e[01;33m\]$(date +%D-%r)\[\e[01;32m\]]\\$ \[\e[0m\]"`

Linux:  
![d05ff131ea443eb296353b30f839cf5b.png](915ff204ff914e9da2a40d2bd56b930f.png)

Windows:  
![244c7a03176ca54c5499f3cdf810388b.png](7bfe7304735b49e0ace8146f7ee5ba8c.png)

Screenshots

- Flameshot & Peek  
    ![f7ce4819ae7f905a1769ae03540b48ee.png](d63b7ca988114e37bb1c1b2070ab7a5e.png)