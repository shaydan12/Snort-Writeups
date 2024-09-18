https://tryhackme.com/r/room/snortchallenges2

# Stop the attack and get the flag (which will appear on your Desktop)

&nbsp;

I logged packets for at least one minute:  `sudo snort -dev -l .`

&nbsp;

Using regex, sort, and uniq, I can find the ip and ports that show up and count how often they occur in the packets: `sudo snort -r snort.log.1724351356 | grep -oE '([0-9]{1,3}\.){3}[0-9]{1,3}:[0-9]{1,5}' | sort | uniq -c | sort -nr`

![image](https://github.com/user-attachments/assets/138ca380-ba2e-41b1-a03c-044ec73a1149)

&nbsp;

Services utilizing port 4444 can have legitimate use cases but can also be an indicator of malicious activity.

The port is often used with Metasploit as it is the default listening port.

`sudo snort -r snort.log.1724421910 -X -q | grep ':4444'`

![image](https://github.com/user-attachments/assets/625cc67a-d60b-45ec-a989-5aae5f814f3d)

&nbsp;

Rule: `drop tcp any any <> any 4444 (msg:"REVERSE SHELL DETECTED on port 4444"; sid:1000001; rev:1;)`

To stop the attack: `sudo snort -c <rule file> -q -Q --daq afpacket -i eth0:eth1 -A full`

&nbsp;

The flag will appear shortly:

![image](https://github.com/user-attachments/assets/c215a46f-56be-4370-b697-fd91adaa3170)

<span style="color: #2dc26b;">**Answer: THM{0ead8c494861079b1b74ec2380d2cd24}**</span>

# What is the used protocol/port in the attack?

 
<span style="color: #2dc26b;">**Answer: 4444**</span>

# Which tool is highly associated with this specific port number?

<span style="color: #2dc26b;">**Answer: Metasploit**</span>
