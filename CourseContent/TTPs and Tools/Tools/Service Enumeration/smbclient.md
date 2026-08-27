Used for enumerating and interacting with SMB shares.

| Flag | Purpose                   |
| ---- | ------------------------- |
| -L   | List all available shares |
| -N   | suppress password prompt  |
| -U   | username                  |
example usage 
```
n00blfye@htb$ smbclient \\10.129.42.253\users

Enter WORKGROUP\user's password:
Try "help" to get a list of possible commands.

smb: \> 
```