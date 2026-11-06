remote administration and management is required for survival, that said if it's misconfigured this is a huge way in for us

### SSH
ssh lets you log in remotely through an encrypted tunnel, it is EVERYWHERE. there are 2 versions SSH-1 and SSH-2 version 2 is more secure. 6 authentication methods for SSH
- Password authentication
- Public key authentication
- Hostbased authentication
- Keyboard authentication
- challenge-response authentication
- GSSAPI authentication
#### Public Key Authentication

this uses public private key pair. server has the public key, you have the private key. 

### Default Configuration

only default we really need to be aware of is x11 forwarding which was vulnerable to command injection in version 7.2p1. other than that most options are commented out and need to be manually conifgured

### Dangerous Settings

SSH is one of the most secure protocols currently available, but if you don't configure it properly, it can easily be attacked. below are some settings to be aware of

| Setting                      | Description                                |
| ---------------------------- | ------------------------------------------ |
| `PasswordAuthentication yes` | Allows password-based authentication       |
| `PermitEmptyPasswords yes`   | Allows the use of empty passwords          |
| `PermitRootLogin yes`        | allows to log in as the root user          |
| `Protocol 1`                 | Uses an outdated version of encryption     |
| `X11Forwarding yes`          | Allows X11 forwarding for GUI applications |
| `AllowTcpForwarding yes`     | Allows forwarding of TCP ports             |
| `PermitTunnel`               | Allows tunneling                           |
| `DebianBanner yes`           | Displays a specific banner when logging in |
### Footprinting the Service
[ssh-audit](../../../TTPs%20and%20Tools/Tools/Remote%20Access/ssh-audit.md) is a good tool for auditing ssh, can also use the -v flag to get more information about the service ie version, authentication methods used etc.
you can specify the authentication method with the `-o` flag and using the `Preferred Authentications` option

### [Rsync](../../../TTPs%20and%20Tools/Tools/Remote%20Access/Rsync.md)
Rsync is a fast and efficient tool for locally and remotely copying files. typically just copies files by looking at changes and just sending those. great for backing things up etc. uses port 873 by default and can be configured to use SSH, piggybacking on top of an established SSH server connection.

### R-services
old remote communication service standard replaced by ssh. same story as telnet, old unsecure, clear text. uses port 512, 513, and 514. only accessible through a suite of programs called r-commands. R-commands suite includes the following
- rcp (remote copy)
- rexec (remote execution)
- rlogin (remote login)
- rsh (remote shell)
- rstat
- ruptime
- rwho (remote who)
commonly abused r-commands inculde the following

| Command | Service Daemon | Port | Transport Protocol | Description                                                                                                                                                                                                                                                        |
| ------- | -------------- | ---- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| rcp     | rshd           | 514  | TCP                | Copy a file or directory bidirectionally from the local system to the remote system (or vice versa) or from one remote system to another. It works like the cp command on linux but provides no warning to the user for overwriting existing files on a system     |
| rsh     | rshd           | 514  | TCP                | Opens a shell on a remote machine without a login procedure. Relies upon the trusted entries in `/etc/hosts.equiv` and `.rhosts` files for validation                                                                                                              |
| rexec   | rexecd         | 512  | TCP                | Enables a user to run shell commands on a remote machine. Requires authentication through the use of a username and password through an unencrypted network socket. Authentication is overridden by the trusted entries in `/etc/hosts.equiv` and `.rhosts` files. |
| rlogin  | rlogind        | 513  | TCP                | Enables a user to log in to a remote host over the network. It works similarly to telnet but can only connect to Unix-like hosts. Authentication is overriden by the trusted entries in the `/etc/hosts.equiv` and .`rhosts` files                                 |
R-services is fundamentally unsafe, and `/etc/hosts.equiv` and `.rhosts` are part of the reason, they bypass authentication. 