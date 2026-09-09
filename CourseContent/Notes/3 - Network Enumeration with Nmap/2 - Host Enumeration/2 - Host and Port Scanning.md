6 states a port can be in when scanned with nmap

| State            | Description                                                                                                                                                                                             |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| open             | This indicates that the connection to the scanned port has been established. These connections can be **TCP connections**, **UDP datagrams** as well as **SCTP associations**.                          |
| closed           | When the port is shown as closed, the TCP protocol indicates that the packet we received back contains an `RST` flag. This scanning method can also be used to determine if our target is alive or not. |
| filtered         | Nmap cannot correctly identify whether the scanned port is open or closed because either no response is returned from the target for the port or we get an error code from the target.                  |
| unfiltered       | This state of a port only occurs during the **TCP-ACK** scan and means that the port is accessible, but it cannot be determined whether it is open or closed.                                           |
| open\|filtered   | If we do not get a response for a specific port, `Nmap` will set it to that state. This indicates that a firewall or packet filter may protect the port.                                                |
| closed\|filtered | This state only occurs in the **IP ID idle** scans and indicates that it was impossible to determine if the scanned port is closed or filtered by a firewall.                                           |
### Discovering Open TCP Ports
default parameters are demonstrated below
```
n00blyfe@htb$ nmap -sT --top-ports=1024 <target>

n00blyfe@htb$ sudo nmap -sS --top-ports=1024 <target>
```

`-F` is a fast port scan which will scan the top 100 ports
if you're tracing a packet, clean up your output by disabling icmp echo, dns resolution and arp-ping see below
```
n00blyfe@htb$ sudo nmap 10.129.2.28 -p 21 --packet-trace -Pn -n --disable-arp-ping
```
##### Connect Scan
A connect scan (`-sT`) performs a full TCP handshake, it is highly accurate, but also very loud. Use it if  you need accuracy and can't afford to knock things over on accident.

### Filtered Ports
Typically a port is listed as filtered because a firewall is either dropping or rejecting packets. the `--max-retries` is set equal to 10 by default. a firewall rejecting packets will send an ICMP type3 error code 3 message back (host unreachable)
### Discovering Open UDP Ports
Use `sU` to perform a UDP scan. This can be rough, UDP is stateless so unless the port is configured to respond we don't receive a response. 
if we receive a response of ICMP type 3 the port is listed closed otherwise if we get an ICMP response it is listed as open|filtered 
###### Version Scan
remember `-sV `can grab the version, service name and other details 