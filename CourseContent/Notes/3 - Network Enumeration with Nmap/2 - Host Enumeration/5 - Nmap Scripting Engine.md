the nmap scripting engine (NSE) lets you create scripts in lua to interact with some services
these scripts fall into 14 different categories

| Category  | Description                                                                                                                             |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| auth      | Determination of Authentication credentials                                                                                             |
| broadcast | Scripts, which are used for host discovery by broadcasting and the discovered hosts, can be automatically added to the remaining scans. |
| brute     | executs scripts that try to log in to the respective service by brute-forcing with credentials                                          |
| default   | Default scripts executed by using the -sC option                                                                                        |
| discovery | Evaluation of accessible services.                                                                                                      |
| dos       | These scripts are used to check services for denial of service vulnerabilities and are used less as it harms the services               |
| exploit   | this category of scripts tries to exploit known vulnerabilities for the scanned port                                                    |
| fuzzer    | this uses scripts to identify vulnerabilities and unexpected packet handling by sending different fields, which can take much time      |
| intrusive | intrusive scripts that could negatively affect the target system                                                                        |
| malware   | checks if some malware infects the target system                                                                                        |
| safe      | Defensive scripts that do not perform intrusive and destructive access                                                                  |
| version   | extension for service detection                                                                                                         |
| vuln      | identification of vulnerabilities                                                                                                       |

you can define the desired scripts in the following ways

default
```
n00blyfe@htb$ sudo nmap <target> -sC
```

script category
```
n00blyfe@htb$ sudo nmap <target> --script <category>
```

defined scripts
```
n00blyfe@htb sudo nmap <target> --script <script-name>, <script-name>...
```

can also do an aggressive scan with `-A` which combines `-sV -O --traceroute -sC`
### Vulnerability Assessment
use `--script vuln` to scan for vulnerabilities for example
```
n00blyfe@htb$ sudo nmap 10.129.2.28 -p 80 -sV --script vuln
```