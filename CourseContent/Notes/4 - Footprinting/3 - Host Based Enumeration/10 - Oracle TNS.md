Oracle Transparent Network Substrate. It is a communication protocol that facilitates communication between oracle databases and applications over the network. popular in healthcare, finance, and retail industries. built-in encryption ensures security of data transmitted. it is now suitable for use in 
- name resolution
- connection management
- load balancing
- security
it provides an additional layer of security over the TCP/IP protocol layer.
### Default Configuration
default port is TCP/1521. TNS listener is configured to support various network protocols including: TCP/IP, UDP, IPX/SPX, and AppleTalk. Can be remotely managed in Oracle 8i/9i but not in Oracle 10g/11g.
By default there is some basic security: auth requires hostnames, IP addresses, usernames and passwords. Will also utilize encryption by default. Typical config files `tnsnames.ora` and `listener.ora` located in `$ORACLE_HOME/network/admin` directory. Typically if you see oracle TNS there are other oracle products in use. can blacklist packages by using a PL/SQL Exclusion list. some noteworthy settings

| Setting              | Description                                                                                                             |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| `DESCRIPTION`        | A descriptor that provides a name for the database and its connection type                                              |
| `ADDRESS`            | the network address of the database, which includes the hostname and port                                               |
| `PROTOCOL`           | The network protocol used for communication with the server                                                             |
| `PORT`               | The port number used for communication with the server                                                                  |
| `CONNECT_DATA`       | Specifies the attributes of the connection, such as the service name or SID, protocl, and database instance identifier. |
| `INSTANCE_NAME`      | The name of the database instance the client wants to connect.                                                          |
| `SERVICE_NAME`       | The name of the service that the client wants to connect to                                                             |
| `SERVER`             | The type of server used for the database connection,such as dedicated or shared                                         |
| `USER`               | The username used to authenticate with the database server                                                              |
| `PASSWORD`           | The password used to authenticate with the database server                                                              |
| `SECURITY`           | The type of security for the connection                                                                                 |
| `VALIDATE_CERT`      | Whether to validate the certificate using SSL/TLS                                                                       |
| `SSL_VERSION`        | The version of SSL/TLS to use for the connection.                                                                       |
| `CONNECT_TIMEOUT`    | The time limit in seconds for the client to establish a connection to the database                                      |
| `RECEIVE_TIMEOUT`    | The time limit in seconds for the client to receive a response from the database                                        |
| `SEND_TIMEOUT`       | The time limit in seconds for the client to send a request to the database                                              |
| `SQLNET.EXPIRE_TIME` | the time limit in seconds for the client to detect a connection has failed                                              |
| `TRACE_LEVEL`        | the level of tracing for the database connection                                                                        |
| `TRACE_DIRECTORY`    | The directory where the trace files are stored.                                                                         |
| `TRACE_FILE_NAME`    | The name of the trace file.                                                                                             |
| `LOG_FILE`           | the file where the log information is stored                                                                            |
[ODAT](../../../TTPs%20and%20Tools/Tools/Exploitation%20Frameworks/ODAT.md) (oracle database attacking tool) will be your BFF for things like this. It is an opensource pentesting tool written in python designed to enumerate and exploit vulnerabilities in oracle databases. 
after an nmap scan we want to find the System ID's (SID) for the database, we can brute force it with nmap, [hydra](../../../TTPs%20and%20Tools/Tools/Brute%20Force/hydra.md), and odat.
if you get creds for an oracle database use [SQLplus](../../../TTPs%20and%20Tools/Tools/Database%20Interaction/SQLplus.md) to connect to it