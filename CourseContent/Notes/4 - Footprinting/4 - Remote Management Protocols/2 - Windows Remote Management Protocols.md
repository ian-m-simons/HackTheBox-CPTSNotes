there are 3 means of remote management for Windows server by default 
- remote desktop protocol (`RDP`)
- Windows Remote Management (`WinRM`)
- Windows Management Instrumentation (`WMI`)
### RDP

RDP typically uses TLS however windows system's do not require it. it is turned on by default on windows server. By default requires network level authentication

### Footprinting the serivce

Nmap can determine if NLA is enabled. be aware that RDP cookies used by nmap can be used to lock ups out by threat hunters and defenders. use RDP-sec-check.pl to check security of RDP servers
login to RDP with xfreerdp, rdesktop, or Remmina (xfreerdp3?)

### WinRM
uses simple object access protocol, must be manually enabled and configured starting on windows 10, uses TCP port 5985 and 5986 (the latter using https) it is on by default for windows server 2012+

### Footprinting the Service
this will show up as microsoft httpapi httdp (SSDP/UPnP) in nmap
to test if WinRM is enabled use test-wsman

### WMI
allows read and write access to almost all settings on windows systems. not a single program, but consists of several programs and various databases (repositories)
### Footprinting the service

uses TCP port 135. use impacket modules to interact with it