Nmap is one of the most common network scanning tools. Below is a basic scan on the top 1,000 most common ports. By default nmap will run a TCP scan unless specifically requested to perform a UDP scan. 
``` 
n00blyfe@htb$ nmap 10.129.42.253

Starting Nmap 7.8 (https://nmap.org) at 2021-02-25 12:25 EST
Nmap scan report for 10.129.42.253
Host is up (0.11s latency).
Not show: 995 closed porst
PORT    STATE SERVICE
21/tcp  open  ftp
22/tcp  open  ssh
80/tcp  open  http
129/tcp open  netbios-ssn
445/tcp open  microsoft-ds

Nmade done: 1 IP adress (1 host up) scanned in 2.19 seconds
```
in this example output we have the port, state and service, the port is pretty self-explanatory, port number along with TCP or UDP (remember we have to force a UDP scan) the state tells us if the port is indeed open you will sometimes see closed of filtered. Filtered typically means there's a firewall only allowing access to the ports from specific addressses. the service heading tells us the service's name. Notably this is not a banner grab and check, this is just what is traditionally mapped to that port. unless we insruct nmap to interact with the service and attempt to tease out identifying info, it COULD be another service all together. Below are some common useful flags for Nmap

| Flag  | Purpose                                                                |
| ----- | ---------------------------------------------------------------------- |
| `-sC` | Scripts - Used to run nmap scripts to obtain more detailed information |
| `-sV` | Version - Perform a version scan                                       |
| `-p`  | Ports - specify ports to scan                                          |
| `-p-` | ALL Ports - specifies that all ports should be scanned                 |
| `-A`  | OS detection                                                           |
| `-oA` | include xml , greppable, and text output                               |
### Nmap Scripts
path to scripts repository is  
`/usr/share/nmap/scripts/`
by default the -sC flag runs many useful default scripts, there are times where you want to run specific scripts, the syntax for that is 
```
n00blyfe@htb$ nmap --script /usr/share/nmap/scripts/<script-name> -p <port-number> <ip address>
```
 default scripts can be found [here](https://nmap.org/nsedoc/categories/default.html) remember, scripts can be loud