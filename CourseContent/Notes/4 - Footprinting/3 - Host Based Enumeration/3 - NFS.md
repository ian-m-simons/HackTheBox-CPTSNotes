This is kind of like SMB for linux/unix in v3 the computer must authenticate, in v4 the user must athenticate.

| Version | Features                                                                                                                                                                                                                                                             |
| ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| NFSv2   | It is older but is supported by many systems and was initially operated entirely over UDP.                                                                                                                                                                           |
| NFSv3   | It has more features, including variable file size and better error reporting, but is not fully compatible with NFSv2 clients                                                                                                                                        |
| NFSv4   | It includes kerberos, works through firewalls and on the internet, no longer requires portmappers, supports ACLs, applies state-based operations, and provides performance improvements and high security. It is also the first version to have a stateful protocol. |
only requires one TCP or UDP port (`2049`) to run the service simplifying the use of the protocol across firewalls. based on the Open Network Computing Remote Procedure Call (`ONC-RPC/SUN-RPC`) no Authentication or Authorization mechanism, instead relyies on RPC protocl options. Most common authentication is via UNIX `UID/GID` and group memberships. 
### Default Configuration
`/etc/exports` file contains a table of physical filesystems on an NFS server accessible by clients. The NFS exports table shows which options it accepts thus indicating available options. some options include 

| Option             | Description                                                                                                                                |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `rw`               | Read and write permissions                                                                                                                 |
| `ro`               | Read only permissions                                                                                                                      |
| `sync`             | Synchronous data transfer (a bit slower)                                                                                                   |
| `async`            | Asynchronous data transfer ( a bit faster)                                                                                                 |
| `secure`           | Ports above 1024 will not be used                                                                                                          |
| `insecure`         | Ports above 1024 will be used                                                                                                              |
| `no_subtree_check` | This option idsables the checking of subdirectory trees                                                                                    |
| `root_squash`      | Assigns all permissions to files of root UID/GID 0 to the UID/GID of anonymous, which prevents `root` from accessing files on an NFS mount |
### Dangerous Settings

| Option           | Description                                                                                                         |
| ---------------- | ------------------------------------------------------------------------------------------------------------------- |
| `rw`             | Read and write permissions                                                                                          |
| `insecure`       | Ports above 1024 will be used                                                                                       |
| `nohide`         | If another file system was mounted below an exported directory, this directory is exported by its own exports entry |
| `no_root_squash` | All files created by root are kept with the UID/GID 0                                                               |

### Footprinting the Service
TCP ports 111 and 2049 are the important ones here. we can also get info about the NFS service via RPC. nmap has some useful scripts to run for enumeration. After we find out all we can, we can mount the drive as shown below.
```
n00blyf@htb$ showmount -e 10.129.14.128

Export list for 10.129.14.128:
/mnt/nfs 10.129.14.0/24

n00blyf@htb$ mkdir target-NFS
n00blyf@htb$ sudo mount -t nfs 10.129.14.128:/ ./target-NFS/ -o nolock
n00blyf@htb$ cd target-NFS
n00blyf@htb$ tree .

.
└── mnt 
    └── nfs
        ├── id_rsa 
        ├── id_rsa.pub 
        └── nfs.share 

2 directories, 3 files
```
at this point we can see the Usernames and groups who have access to these files, then we can adapt our system to them and have access to view or modify them as appropriate

