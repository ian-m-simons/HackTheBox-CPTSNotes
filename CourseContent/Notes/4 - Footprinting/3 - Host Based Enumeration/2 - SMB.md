`Server Message Block` (`SMB`) is a client-server protocol that regulates access to files and entire directories and other network resources such as printers, routers, or interfaces released for the network. Typically this is a Windows centric protocol, but samba exists. the SMB server provides porst of its local file system as shares. ACLs control who can access what and they can be fine grained managing full rwx for users and groups.
### Samba
Unix alternative for SMB. uses the Common Internet File System (`CIFS`)network protocol. it is a version of SMB. it lets samba communicate with windows. generally speaking SMB/CIFS is outdated and you should be using SMB 2 or SMB 3 see table below

| SMB Version | Supported                           | Features                                                               |
| ----------- | ----------------------------------- | ---------------------------------------------------------------------- |
| CIFS        | Windows NT 4.0                      | Communication via NetBIOS interface                                    |
| SMB 1.0     | Windows 2000                        | Direct connection via TCP                                              |
| SMB 2.0     | Windows Vista, Windows Server 2008  | Performance upgrades, improved message signing, caching feature        |
| SMB 2.1     | Windows 7, Windows Server 2008 R2   | Locking mechanisms                                                     |
| SMB 3.0     | Windows 8, Windows Server 2012      | Multichannel connections, end-to-end encryption, remote storage access |
| SMB 3.0.2   | Windows 3.1, Windows Server 2012 R2 |                                                                        |
| SMB 3.1.1   | Windows 10, Windows Server 2016     | Integrity checking, AES-128 encryption                                 |
Sambav3 allows full AD domain membership and samba v4 allows AD domain controller. 
### Default Configuration
some noteworthy settings 

| Setting                        | Description                                                           |
| ------------------------------ | --------------------------------------------------------------------- |
| `[sharename]`                  | The name of the network share.                                        |
| `workgroup = WORKGROUP/DOMAIN` | Workgroup that will appear when clients query.                        |
| `path = /path/here`            | the directory to which users is given access.                         |
| `server string = STRING`       | the string that will show up when a connection is initiated.          |
| `unix password sync = yes`     | Synchronize the UNIX password with the SMB password?                  |
| `usershare allow guests = yes` | Allow non-authenticated users to access defined share?                |
| `map to guest = bad user`      | what to do when a user login request doesn't match a valid UNIX user? |
| `browseable = yes`             | Should this share be shown in the list of available shares?           |
| `guest ok = yes`               | Allow connecting to the service without using a password?             |
| `read only = yes`              | Allow users to read files only?                                       |
| `create mask = 0700`           | What permissions need to be set for newly created files?              |
### Dangerous Settings
some settings can introduce vulnerabilities, see the table below

| Setting                     | Description                                                         |
| --------------------------- | ------------------------------------------------------------------- |
| `browseable = yes`          | Allow listing available shares in the current share?                |
| `read only = no`            | Forbid the creating and midification of files?                      |
| `writeable = yes`           | Allow users to cerate and modify files?                             |
| `guest ok = yes`            | Allow ocnnecting to the service without using a password?           |
| `enable privileges = yes`   | Honor privileges assigned to specific SID?                          |
| `create mask = 0777`        | What permissions must be assigned to the newly created files?       |
| `directory mask = 0777`     | What permissions must be assigned to the newly created directories? |
| `logon script = script.sh`  | what script needs to be executed on the user's login?               |
| `magic script = script.sh`  | which script should be executed when the script gets closed?        |
| `magic output = script.out` | Where the output of the magic script needs to be stored?            |

