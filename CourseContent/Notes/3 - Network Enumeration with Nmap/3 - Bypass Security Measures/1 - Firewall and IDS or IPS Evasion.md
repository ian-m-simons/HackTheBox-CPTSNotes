Nmap has plenty of ways to dodge Firewalls and IDS/IPS, lets look at some

### Firewalls
a firewall compares traffic to a predetermined set of rules then decides whether to allow or deny said traffic.

### IDS/IPS
IDS scans the network for potential attacks and reports, IPS does the same, but takes preventative action (namely preventing pending connection attempts)

### Determine Firewalls and Their Rules
remember dropped packets timeout, rejected packets get an RST flag response. When it comes to firewalls our bff is `-sA` which is a TCP ACK scan. firewalls struggle with this cause they don't know who started the conversation so they typically will just let these flags through. remember no response means packets were dropped, ICMP errors (ie host unreachable) mean rejected.

### Detect IDS/IPS
it is recommended to use several virtual private servers (VPS) with different IP addresses to determine whether such systems are on the target network during a penetration test. If an administrator detects such a potential attack, they will block the IP themselves, then potentially notify their ISP which will block said IP from all internet access.
- we can intentionally trigger IDS by being super loud, ie aggressively scanning a single port. to see what happens
- One method is to scan from a VPS. if the the VPS is blocked and can no longer access the target network, we know that either IPS or an admin has taken some security measures. 
### Decoys
`-D` this is a method of obfuscating yoeur IP address, as nmap will insert random IP addresses into the IP header to disguise the origin. we can als use `RND` to specify the number of random IP addresses, separated by a `:` the Decoys must be alive otherwise the service on the target may be unreachable due to SYN-flood security mechanisms. see the attached example.

```
n00blyfe@htb$ sudo nmap 10.129.2.28 -p 80 -sS -Pn -n --disable-arp-ping --packet-trace -D RND:5  

Starting Nmap 7.80 ( https://nmap.org ) at 2020-06-21 16:14 CEST 
SENT (0.0378s) TCP 102.52.161.59:59289 > 10.129.2.28:80 S ttl=42 id=29822 iplen=44  seq=3687542010 win=1024 <mss 1460> 
SENT (0.0378s) TCP 10.10.14.2:59289 > 10.129.2.28:80 S ttl=59 id=29822 iplen=44  seq=3687542010 win=1024 <mss 1460> 
SENT (0.0379s) TCP 210.120.38.29:59289 > 10.129.2.28:80 S ttl=37 id=29822 iplen=44  seq=3687542010 win=1024 <mss 1460> 
SENT (0.0379s) TCP 191.6.64.171:59289 > 10.129.2.28:80 S ttl=38 id=29822 iplen=44  seq=3687542010 win=1024 <mss 1460> 
SENT (0.0379s) TCP 184.178.194.209:59289 > 10.129.2.28:80 S ttl=39 id=29822 iplen=44  seq=3687542010 win=1024 <mss 1460> 
SENT (0.0379s) TCP 43.21.121.33:59289 > 10.129.2.28:80 S ttl=55 id=29822 iplen=44  seq=3687542010 win=1024 <mss 1460> 
RCVD (0.1370s) TCP 10.129.2.28:80 > 10.10.14.2:59289 SA ttl=64 id=0 iplen=44  seq=4056111701 win=64240 <mss 1460> 
Nmap scan report for 10.129.2.28 
Host is up (0.099s latency). 

 PORT   STATE SERVICE 
 80/tcp open  http 
 MAC Address: DE:AD:00:00:BE:EF (Intel Corporate)  
 
 Nmap done: 1 IP address (1 host up) scanned in 0.15 seconds`
```
Often Decoy packets get filtered by ISP's and routers. you can also use the -S to specify the source if you need to fake a specific subnet etc. for example if we wanted to scan 10.129.2.28 but appear to be coming from a different subnet we could do the following. spoofing ourselves as 192.168.1.69
```
n00blyfe@htb$ sudo nmap -S 192.168.1.69 -sC -sV 10.129.2.28
```

### DNS Proxying
Nmap does a reverse DNS lookup, you can specify which dns server to use with `--dns-server <dns-server>` you can also change your source port to bypass firewalls essentially use TCP port 53 firewall assumes it's DNS and lets you through, to do this use `--source-port`

if you can access by changing source port to 53 you can probably do other things with the same method and IDS/IPS is probably struggling