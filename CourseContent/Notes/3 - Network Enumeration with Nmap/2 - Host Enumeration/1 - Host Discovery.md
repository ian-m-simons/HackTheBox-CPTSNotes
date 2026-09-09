the simplest and most effective means of host discovery is to use ICMP echo requests. ALWAYS STORE THE OUTPUT FROM EVERY SCAN.  
### Scan network range
```
n00blyfe@htb$ sudo nmap -sn -oA tnet 10.129.2.0/24 | grep for | cut -d" " -f5

10.129.2.4
10.129.2.10
10.129.2.11
10.129.2.18
10.129.2.19
10.129.2.20
10.129.2.28
```

ok significant takeaways from this example:
- `10.129.2.0/24` scans the whole
- -sn disables port scanning (ping sweep)
- -oA tnet stores results in ALL formats using the name tnet (ie tnet.json, tnet.nmap etc)
### Scan IP List
you can add an input list with the `-iL` command. Typcially list will be something like `hosts.lst` which will be `\n` delimited list of IP addresses

### Scan multiple IPs
both of the following are valid ways to scan multiple targets
```
n00blyfe@htb$ nmap -sn -oA tnet 10.129.2.18 10.129.2.19 10.129.2.20

n00blyfe@htb$ nmap -sn -oA tnet 10.129.2.18-20
```

### Scan Single IP
ensure a host is alive before we scan open ports
```
n00blyfe@htb$ sudo nmap -sn -oA host 10.129.2.18

starting Nmap 7.8 ( https://nmap.org ) at 2020-06-14 23:59 CEST
Nmap scan report for 10.129.2.18
Host is up (0.087s latency).
MAC Address: DE:AD:00:00:BE:EF
Nmap done: 1 IP address (1 host up) scanned in 0.11 seconds
```

in addition to an ICMP Ping we can perform an arp ping to see if hosts are up. remember arp is L2 and can't cross routers or above and it is also broadcast.