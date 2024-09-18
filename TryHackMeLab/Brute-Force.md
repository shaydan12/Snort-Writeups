https://tryhackme.com/r/room/snortchallenges2

# Stop the attack and get the flag (which will appear on your Desktop)

&nbsp;

Log the packets to analyze the traffic: <span style="color: #ffffff;">sudo snort -dev -l .</span>

&nbsp;

Using regex, sort, and uniq, I can find the ip and ports that show up and count how often they occur in the packet: `sudo snort -r snort.log.1724351356 | grep -oE '([0-9]{1,3}\.){3}[0-9]{1,3}:[0-9]{1,5}' | sort | uniq -c | sort -nr`

There is an unusually large amount of packets associated with port 22 (SSH)

![image](https://github.com/user-attachments/assets/e5898a46-15d4-47b8-9003-15e48d768484)

&nbsp;

&nbsp;

While doing some further investigations, I found hints of ssh bruteforce: sudo snort -r &lt;snort log&gt; -X -n 30

![image](https://github.com/user-attachments/assets/7b739e5f-d134-404e-89f7-c81d1c1a554c)

&nbsp;

Rule: `drop tcp any any <> any 22 (msg: "preventing SSH access"; sid: 100001; rev:1;)`

To stop the attack: `sudo snort -c <rule file> -q -Q --daq afpacket -i eth0:eth1 -A full`

&nbsp;

&nbsp;

<span style="color: #2dc26b;">**Answer: THM{81b7fef657f8aaa6e4e200d616738254}**</span>

# What is the name of the service under attack?

&nbsp;

&nbsp;

<span style="color: #2dc26b;">**Answer: ssh**</span>

# What is the used protocol/port in the attack?

![image](https://github.com/user-attachments/assets/6b2e6bf6-2295-4639-b9e4-8ed164cdba8a)

&nbsp;

&nbsp;

<span style="color: #2dc26b;">**Answer: tcp/22**</span>
