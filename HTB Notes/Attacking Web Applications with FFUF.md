   

Attacking Web Applications with FFUF

What is Fuzzing?

- Fuzzing is a testing technique that sends various types of user input to study how it reacts
- Fuzzing utilizes wordlists to reveal pages
- See GitHub SecList repository for more wordlists
- IMPORTANT:![c17c4c8fb75c0bac4e27161b9f574af5.png](268e92f1315a4df09b9c34dc5cbab699.png)
- IMPORTANT: ![f0d20f29b1ae1491f0b8561a6d757dab.png](b635d77c0a2f42b48ca9047bad860c65.png)

---

HTTP Codes  
404 Not Found  
403 Access Denied

---

To Install:

- apt install ffuf -y

---

![69ee2ca1a9c6a3ca071e8340d86a3bde.png](e53748851bb74307bbf0d33c85bb7303.png)

---

![0fa769749796f243341b5b0514f69fbd.png](f7e99e5380744daaa200c6040fcbaa81.png)

- fuff -h command  
    ![7cfa54dc67582829af5f2dba6827445c.png](256c3fec23db4c35bf34276b29d87d4a.png)

---

Directory Fuzzing  
![5ee6979494bc50dfcb55c7169025694c.png](40c0f0829b0446ae886d81f90fdc4823.png)

- Add in: ![185818d34d6081f26e7d8e2d40c5a570.png](edf39f4dc7ab4db9b50d4a909807619c.png)
- NOTE: adding in -t 200 increases the # of threads to 200. Could cause DOS

---

Extension Fuzzing

- Used to find directories containing any hidden pages.  
    apache = .php , .phps , .php3  
    IIS = .asp , .aspx  
    ![b562a8b6ac7e76cd2c0c04d907687beb.png](db2cbfa2b57a4a4fbf7d20982bce4e5c.png)

1. Run command
2. Any 200s means it runs on that particular server type
3. Begin Page Fuzzing

---

Page Fuzzing  
NOTE: Uses the same wordlist as directory fuzzing

- Used to find hidden pages  
    ![9359c5b09325902f8c6024a42a0a8df3.png](0c0ee90609244770a2778bfdcdcf1bc7.png)

---

Recursive Fuzzing

- The process of fuzzing for directories, then finding extensions then files is time consuming
- `ffuf -w [wordlist path.txt:FUZZ] -u http://Server_IP:Port/FUZZ -recursion -recursion-depth 1 -e .php -v`

---

Sub-domain Fuzzing

- used for any *.website.com
- Choose the appropriate wordlist and a target
- Can only find public domains

---

Vhost Fuzzing

- Works by the fact that a single IP could be serving two or more different websites  
    ![5136bd76dbfe64a3209b153e5e7ff9e0.png](3744280fb8474937a36b69f0ae6ea5b3.png)

---

![d6b43f1456469dad0d710a5b853abd98.png](753aad80a8cd4d729583731187bde968.png)

![4cfca60c009cdf583c0b1ec523a4152d.png](fa32e532c4fd4528abcb4e02152be1ab.png)