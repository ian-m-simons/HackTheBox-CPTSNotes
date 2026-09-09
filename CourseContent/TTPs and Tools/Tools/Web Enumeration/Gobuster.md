Gobuster is a versatile tool used for DNS, Vhost, and directory brute-forceing. it can also handle other various tasks such as AWS public S3 bucket enumeration. Review your status codes as those will be used here (see example output below).
modes 

| Mode  | Use                                         |
| ----- | ------------------------------------------- |
| dir   | enumerate directories and files             |
| dns   | discover subdomains, through DNS resolution |
| s3    | enumerate Amazon s3 buckets                 |
| gcs   | enumerate google cloude storage buckets     |
| vhost | Discover virtual hosts on web servers       |
| fuzz  | custom fuzzing with the fuzz keyword        |
| tftp  | Enumerate files on TFTP servers             |
important flags

| Flag | Use                      |
| ---- | ------------------------ |
| -w   | specify word list to use |

```
n00blyfe@htb[/htb]$ gobuster dir -u http://10.10.10.121/ -w /usr/share/seclists/Discovery/Web-Content/common.txt

===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.10.121/
[+] Threads:        10
[+] Wordlist:       /usr/share/seclists/Discovery/Web-Content/common.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2020/12/11 21:47:25 Starting gobuster
===============================================================
/.hta (Status: 403)
/.htpasswd (Status: 403)
/.htaccess (Status: 403)
/index.php (Status: 200)
/server-status (Status: 403)
/wordpress (Status: 301)
===============================================================
2020/12/11 21:47:46 Finished
===============================================================
```

| Code | Meaning                                               |
| ---- | ----------------------------------------------------- |
| 1xx  | Informational                                         |
| 100  | Continue                                              |
| 101  | switching protocols                                   |
| 102  | processing                                            |
| 103  | deprecated                                            |
| 2xx  | success                                               |
| 200  | ok (standard success)                                 |
| 201  | created                                               |
| 202  | accepted                                              |
| 203  | Non-AUthoritative information                         |
| 204  | no content                                            |
| 205  | reset content                                         |
| 207  | multi-status (expect multiple response codes in body) |
| 208  | already reported (in a 207 body)                      |
| 226  | instance-manipulations used                           |
| 3xx  | redirect                                              |
| 300  | multiple choices (on redirection)                     |
| 301  | moved permanently                                     |
| 302  | found (alternate url in location field of header)     |
| 303  | see other                                             |
| 304  | not modified                                          |
| 305  | use proxy                                             |
| 306  | switch proxy (deprecated)                             |
| 307  | temporary redirect                                    |
| 4xx  | client error                                          |
| 400  | bad request                                           |
| 401  | unauthorized                                          |
| 402  | payment required (not typically in use)               |
| 403  | forbidden                                             |
| 404  | not found                                             |
| 405  | method not allowed                                    |
| 406  | not acceptable                                        |
| 5xx  | server side error                                     |
| 500  | internal server error                                 |
| 501  | not ipmlemented                                       |
| 502  | bad gateway                                           |
| 503  | service unavailable                                   |
| 504  | gateway timeout                                       |
