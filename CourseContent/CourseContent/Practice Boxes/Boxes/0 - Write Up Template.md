# \<Machine Name\> - Hack the Box
**Difficulty:** \<Easy/Medium/Hard/Insane\>
**OS:** \<Linux/Windows\>
**Points:** \<XX\>
**Date Completed:** \<YYYY-MM-DD\>
**Write-up Authored by:** Ian Simons
**Challenge Created by:** \<challenge author\>
**Core Competencies:**
- \<skill 1\>
- \<skill 2\>
- \<skill 3 - continue as needed\>

---
## Overview
\<3-5 sentence (capped at 7 for large labs/boxes) overview/executive summary of the machine, primary attack path, and key takeaways\>
Note: Flags documented in Appendix B

---
Vulnerability summary

| Vulnerability                   | CVE                      | CVSS Score | MITRE ATT&CK Tactic/Technique | Location                                         |
| ------------------------------- | ------------------------ | ---------- | ----------------------------- | ------------------------------------------------ |
| \<short name of Vulnerability\> | \<CVE-YYYY-XXXX\> or N/A | X.X        | \<tactic-technique ID: Name\> | \<Initial Access / privilege escalation / etc \> |

---
## Attack Path Summary
1. \<high level overview\>
2. \<of all steps used\>
3. \<to go from\>
4. \<no access\>
5. \<to basic access\>
6. \<to full root/system access\>
---
## Reconnaissance
### Port Discovery
```
n00blyfe@localHost$ nmap -sC -sV -oN scan.txt -T4 <Target-IP-Address>
<output of scan>
```

#### Key Open Ports and Services
 - \<Port/\[TCP | UDP\]\> - \<Service\> (\<Version if known\>)
 - \<Port/\[TCP | UDP\]\> - \<Service\> (\<Version if known\>)
 - \<Port/\[TCP | UDP\]\> - \<Service\> (\<Version if known\>)

### Service Enumeration
\<Data to be Used - directory/file discovery results, interesting findings, technologies identified, credentials or low hanging fruit discovered\>
### Web Enumeration 
```
n00blyfe@localHost$ <any commands run for enumaration ie gobuster ffuz etc>
```
- \<discovery 1\>
- \<discovery 2\>
- \<discover 3 - continue as needed\>

### Vulnerability Research
- \<vulnerable target - CVE if applicable\>
- \<vulnerable target - CVE if applicable\>
- \<vulnerable target - CVE if applicable\>

---
## Initial Access
### Vulnerability Details
- Description: \<Data to be used - concise description of the vulnerability\>
- CVE: \<CVE-YYYY-XXXX or N/A\>
- CVSS score: \<X.X (severity)\>
- MITRE ATT&CK: \<Tactic - Technique ID: Name\>(example Initial Access - T1190: Exploit Public-Facing Application)
#### Exploitation Steps
1. \<step 1\>
2. \<step 2\>
3. \<step 3 - continue as needed\>
#### Key Commands / Payloads
```
n00blfye@localHost$ <commands used or relevant payload snippets etc>
```

#### Proof of Access 
##### Screenshots
\<images as needed\>
##### Validation commands
```
whoami id or other commands used to prove I was indeed on the system in question
```

---
## Privilege Escalation 
### Enumeration Findings
\< data to be used - key results from linpeas/winpeas, suid, sudo, credentials, misconfigurations etc\>
### Vulnerability Details
- Description: \<Data to be used - concise description of the vulnerability\>
- CVE: \<CVE-YYYY-XXXX or N/A\>
- CVSS score: \<X.X (severity)\>
- MITRE ATT&CK: \<Tactic - Technique ID: Name\>(example Initial Access - T1190: Exploit Public-Facing Application)
#### Exploitation Steps
1. \<step 1\>
2. \<step 2\>
3. \<step 3 - continue as needed\>
#### Key Commands / Payloads
```
n00blfye@localHost$ <commands used or relevant payload snippets etc>
```

#### Proof of Privileges 
```
whoami or other proof of root/SYSTEM
```
---
## Lessons Learned & Notes
\<quick paragraph (no more than 7 sentences absolute tops) about the room, what I learned, why I chose it etc. \>
- \<Key takeaway 1\>
- \<Key takeaway 2\>
- \<Key takeaway 3 - continue as needed\>
- \<What worked well\>
- \<What did not work well\>
- \<What went faster/slower than expected\>
- \<Rabbit holes encountered\>
- \<Techniques or tools to remember for similar boxes\>
---
## Appendix
### Appendix A
#### Tools Used 
- \<tool 1\>
- \<tool 2\>
- \<tool 3\ - continue as needed> 
### Appendix B
#### Flags found
- \<flag\*\*\*\*\*\*\*\*\*1\>
- \<flag\*\*\*\*\*\*\*\*\*2\>
-  \<flag\*\*\*\*\*\*\*\*\*3\>
### Appendix C
#### Supporting Evidence
- \<Any other evidence found\>
- \<include screenshots\>
- \<include files or at least snippets from files\>
- \<anything else important\>
- \<this section also functions as a catchall\>
