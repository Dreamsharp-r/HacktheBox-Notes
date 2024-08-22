   

Working with IDS/IPS

Suricata Fundamentals  
sudo suricata-update // update the ruleset  
sudo suricata-update list-sources // list all ruleset providers  
sudo suricata-update enable-source [source. ex. et/open] // enable a ruleset within suricata rules  
sudo systemctl restart suricata // restart the suricata service  
sudo suricata -T -c /etc/suricata/suricata.yaml // validate suricata configuration

---

Suricata Modes (How Suricata will operate):

- IDS Mode
- IPS Mode
- IDPS Mode
- Network Security Monitoring (NSM) Mode

---

Suricata Inputs (How Suricata ingest data):

1. Offline Input (Read from an already made PCAP file)

- suricata -r /[filepath/filename.pcap]
- suricata -r /[filepath/filename.pcap] -k none -l [directory]
    - the k flag indicate bypass checksum
    - the l flag to log in a different directory

2. Live Input:

- LibPcap mode (live inputs. Performance limited)
    1. ifconfig to find the interface
    2. sudo suricata --pcap=[interface] -vv
- NFQ mode (inline operations. Linux specific)
    1. sudo iptables -I FORWARD -j NFQUEUE
    2. sudo suricata -q 0
- IDS mode w/ AF_PACKET input (inline operations.Best. However incomptiable w/ older linux distro)
    - sudo suricata -i [interface]  
        OR
    - sudo suricata --af-packet=[interface]

---

Observing LIVE traffic from a file:

1. Establish an additional connection
2. sudo tcpreplay -i [interface] [filepath.file.pcap]
3. Logs available at /var/log/suricata

---

Suricata Outputs:  
Creates the following default logs

1. eve.json

- Creates JSON objects w/ timestamps, flow_id, events

3. fast.log

- Records only alerts

5. stats.log

- Debugging log

Suricata Log Language:  
cat /var/log/suricata/eve.json | jq -c 'select(.event_type == "keyword")'  
cat /var/log/suricata/eve.json | jq -c 'select(.event_type == "keyword")' | head -1 -jq .

- flow_id: Unique identifier assigned to each network packet flow
- pcap_cnt: counter to identify the source of a packet

---

File Extraction (capture & store file)

1. File changes in the suricata.yaml file.  
    ![5854e69a5fb4b9cfd4e23a0949d86dfd.png](cba72aeece27414292a7d580129d35e5.png)
2. Set the dir option to your choice within file-store
3. Configure the rules to instruct Suricata what files to extract
4. run Suricata. suricata -r /home/htb-student/pcaps/vm-2.pcap
5. Creates the eve.json, fast, stat, and suricata log along with filestore directory
6. Files are stored as SHA256

---

Live Rules within Suricata (Updating our ruleset w/o interrupting ongoing traffic)

1. suricata.yaml file  
    ![915cbed726a9dd4b621879051cd98a4f.png](809afbd0fe4b46bc93996cf6cd6bafbd.png)
2. Send a kill command.  
    ![7357da64169594bb7ad34404d0db4b16.png](f03e2b06f2384015864651663c793071.png)

![b4622da3aadf11800959462fe2b4642b.png](10734c63726d469283bd58868d9149ac.png)

Fenix5@htb[/htb]$ sudo snort -c /root/snorty/etc/snort/snort.lua --daq-dir /usr/local/lib/daq -r /home/htb-student/pcaps/icmp.pcap

Fenix5@htb[/htb]$ sudo snort -c /root/snorty/etc/snort/snort.lua --daq-dir /usr/local/lib/daq -r /home/htb-student/pcaps/icmp.pcap -A cmg

$ cat conn.log | /usr/local/zeek/bin/zeek-cut id.orig_h id.resp_h orig_bytes | sort | grep 178.23.155.240 | datamash -g 1,2 sum 3

![9c15feff9cd78a0ba511649245c2e695.png](2e3a9249346b4528b4e9bad1b1d74d67.png)

![f313eaa5d8a2304c6d97fcff383bd10f.png](d8b25e3f2f4e4c66b596608641bbcefb.png)