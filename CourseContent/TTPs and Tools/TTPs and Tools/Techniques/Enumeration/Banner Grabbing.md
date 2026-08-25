Banner grabbing is used to gather information about computer systems, software versions etc running on open network ports. When you connect to a service, typically a text banner will be displayed revealing information and that is what we are after. Example
```shell
n00blyfe@htb$ netcat 10.10.10.10 22

SSH-2.0-OpenSSH_8.4p1 Debian-3
```
in this example we connected to the target machine on port 22 using netcat and the banner revealed the service running, what version was being used, the operating system, and the OS version. All of this could be potentially valuable information. 
### Tools
1. [[Netcat]]
2. [[Telnet]]
