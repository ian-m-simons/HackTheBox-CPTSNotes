Nmap results 
```
┌─[us-dedivip-3]─[10.10.14.169]─[n00blyfe@htb-su51vunztf]─[~]
└──╼ [★]$ sudo nmap -sC -sV -oN scan.txt -p- 10.129.62.162
Starting Nmap 7.95 ( https://nmap.org ) at 2026-08-30 06:30 EDT
Nmap scan report for 10.129.62.162
Host is up (0.0071s latency).
Not shown: 65534 filtered tcp ports (no-response)
PORT     STATE SERVICE VERSION
8080/tcp open  http    Apache Tomcat/Coyote JSP engine 1.1
|_http-title: Apache Tomcat/7.0.88
|_http-favicon: Apache Tomcat
|_http-server-header: Apache-Coyote/1.1

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 116.21 seconds


```

searchsploit results

```
┌─[us-dedivip-3]─[10.10.14.169]─[n00blyfe@htb-su51vunztf]─[~]
└──╼ [★]$ searchsploit -j apache tomcat 7.0.88
{
	"SEARCH": "apache tomcat 7.0.88",
	"DB_PATH_EXPLOIT": "/usr/share/exploitdb",
	"RESULTS_EXPLOIT": [
		{"Title":"Apache Tomcat < 9.0.1 (Beta) / < 8.5.23 / < 8.0.47 / < 7.0.8 - JSP Upload Bypass / Remote Code Execution (1)","EDB-ID":"42953","Date_Published":"2017-09-20","Date_Added":"2017-10-04","Date_Updated":"2017-10-04","Author":"xxlegend","Type":"webapps","Platform":"windows","Port":"","Verified":"0","Codes":"CVE-2017-12615","Tags":"","Aliases":"","Screenshot":"","Application":"","Source":"https://bz.apache.org/bugzilla/show_bug.cgi?id=61542#c0","Path":"/usr/share/exploitdb/exploits/windows/webapps/42953.txt"},
		{"Title":"Apache Tomcat < 9.0.1 (Beta) / < 8.5.23 / < 8.0.47 / < 7.0.8 - JSP Upload Bypass / Remote Code Execution (2)","EDB-ID":"42966","Date_Published":"2017-10-09","Date_Added":"2017-10-09","Date_Updated":"2021-04-14","Author":"intx0x80","Type":"webapps","Platform":"jsp","Port":"","Verified":"1","Codes":"CVE-2017-12617","Tags":"","Aliases":"","Screenshot":"","Application":"","Source":"https://github.com/cyberheartmi9/CVE-2017-12617","Path":"/usr/share/exploitdb/exploits/jsp/webapps/42966.py"}
	],
	"DB_PATH_SHELLCODE": "/usr/share/exploitdb",
	"RESULTS_SHELLCODE": [	]
}


```

CVE's for apache tomcat 7.0.88
	CVE-2017-12617 & CVE-2017-12615

demo creds from error message still in use
user: tomcat
pass:s3cret


user flag: 7004dbcef0f854e0fb401875f26ebd00
root flag: 04a8b36e1545a455393d067e772fe90e

remember metasploit can do more than just exploit and escalate, it can also brute force scan etc
info command will give you a quick run down of the module as well as the options available

