 FTP is an application layer protocol (like http or pop). FTP uses 2 channels Port 21 for control Port 22 for data transmission. in active mode, the clienty tells the server send data to port XXXXX, however firewalls block this so passive mode the server tells the client to connect to port XXXXX to establish the data channel. FTP can be a little bit of the wild west with servers varying on which commands they do or do not support. typically client sends request and the server will respond with a status code. remember FTP is clear-text not encrypted. You will need FTP credentials, though sometimes you can login anonymously. 
### TFTP
simpler version of ftp but no authentication, and uses UDP. Can only be used locally in a protected network. TFTP commands include the following 

| Commands | Description                                                                                                                            |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Connect  | Sets the remote host, and optionally the port, for file transfers.                                                                     |
| get      | Transfers a file or set of files from the remote host to the local host.                                                               |
| put      | transfers a file or set of files from the local host onto the remote host.                                                             |
| quit     | exits tftp                                                                                                                             |
| status   | Shows the current status fo tftp, including the current transfer mode (ascii or binary), connection status, time-out value, and so on. |
| verbose  | turns on verbose mode or or off, which displays additional information during file transfer.                                           |
TFTP does not ahve a directory listing functionality

### Default Configuration
vsFTPd is the most common linux-based FTP server. settings are in /etc/vsftpd.conf. view the man page to find all possible settings. The default settings are listed below

| setting                                                        | Description                                                                                               |
| -------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `listen=NO`                                                    | Run from inetd or as a standalone daemon?                                                                 |
| `Listen_ipv6=YES`                                              | Listen on IPv6?                                                                                           |
| `anonymous_enable=NO`                                          | Enable Anonymous access?                                                                                  |
| `local_enable=YES`                                             | Allow local users to login?                                                                               |
| `dirmessage_enable=YES`                                        | Display active directory messagse when users go into certain directories?                                 |
| `use_localtime=YES`                                            | Use local time?                                                                                           |
| `xferlog_enable=YES`                                           | Activate logging of uploads/downloads?                                                                    |
| `connect_from_port_20=YES`                                     | connect from port 20?                                                                                     |
| `secure_chroot_dir=/var/run/vsftpd/empty`                      | Name of an empty directory                                                                                |
| `pam_service_name=vsftpd`                                      | This string is the name of the PAM service vsftpd will use.                                               |
| `rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem`           | The last three rows here specify the location of the RSA certificate to use for SSL encrypted connections |
| `rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key'` |                                                                                                           |
| `ssl_enable=NO`                                                |                                                                                                           |
### Dangerous settings
typically here we're talking about optional anonymous settings see the table below

| setting                        | description                                                                        |
| ------------------------------ | ---------------------------------------------------------------------------------- |
| `anonymous_enable=YES`         | Allowing anonymous login?                                                          |
| `anon_upload_enable=YES`       | Allowing anonymous to upload files?                                                |
| `anon_mkdir_write_enable=YES`  | Allowing anonymous to create new directories?                                      |
| `no_anon_password=YES`         | Do not ask anonymous for password?                                                 |
| `anon_root=/home/username/ftp` | Directory for anonymous                                                            |
| `write_enable=YES`             | Allow the usage of FTP commands: STOR, DELE, RNFR, RNTO, MKD, RMD, APPE, and SITE? |
tl;dr don't allow anonymous access to things. 
Make sure you turn on hide_ID so that anonymous users can't find usernames to attack.
remember that internal systems are not typically adequately hardened. 
### Footprinting the Service
typically we will footprint using the nmap scripting engine. much of this process was covered in the previous module, notably though if it is Secure FTP (with TLS bolted on) you'll need to use openssl instead of netcat.