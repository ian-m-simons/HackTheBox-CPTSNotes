U Used for enumerating and interacting with SMB shares. 

| Flag | Purpose                                         |
| ---- | ----------------------------------------------- |
| -L   | List all available shares                       |
| -N   | suppress password prompt/null session/anonymous |
| -U   | username                                        |
post login commansd to be aware of 

| Command      | Purpose                                                                |
| ------------ | ---------------------------------------------------------------------- |
| `help`       | List available commands                                                |
| `get`        | Download files or folders                                              |
| `!<command>` | execute local system command (ie !ls would run ls on the local system) |
| `smbstatus`  | shows who is connected, version in use, IP's etc                       |
example usage 
```
n00blfye@htb$ smbclient \\10.129.42.253\users

Enter WORKGROUP\user's password:
Try "help" to get a list of possible commands.

smb: \> 
```