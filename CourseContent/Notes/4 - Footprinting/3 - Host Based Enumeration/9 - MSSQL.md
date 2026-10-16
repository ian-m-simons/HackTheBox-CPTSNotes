Microsoft's dbms, proprietary/closed-source. populare when you also have to work with .NET, can be run on linux or mac but most common in microsoft.

### MSSQL Clients
SQL Server Management Studio (SSMS) is an optional feature for the client that can be installed. It is commonly used for config and management. This introduces additional vulnerabilities to the database on client workstations. other clients include:
- mssql-cli
- SQL Server PowerShell
- HeidiSQL
- SQLPro
- Impacket's mssqlclient.py

Impacket's mssqlclient.py is probably going to be the one you use the most just by virtue of it being in kali and parrot by default.

### MSSQL Databases 
default databases are here, they can help better understand things

| Default System Database | Description                                                                                                                                                                                           |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| master                  | Tracks all system information for an SQL server instance                                                                                                                                              |
| model                   | Template database that acts as a structure for every new database created. Any setting changed in the model database will be reflected in any new databes created after changes to the model database |
| msdb                    | The SQL Server Agent uses this database to schedule jobs & alerts                                                                                                                                     |
| tempdb                  | Stores temporary objects                                                                                                                                                                              |
| resource                | Read-only database containing system objects included with SQL server                                                                                                                                 |
### Default Configuration

by default the SQL service will run as NT SERVICE\MSSQLSERVER and will not enforce encryption. Authentication is handled via windows either locally or using AD.
### Dangerous Settings
look for the following
- MSSQL clients not using encryption to connect to the MSSQL server
- The use of self-signed certificates when encryption is being used. It is possible to spoof self-signed certificates
- the use of named pipes
- weak and default sa credentials. Admins may forget to disable this account
### Footprinting the service
nmap has some default mssql scritps which can target the default port 1433. 
also a good metsploit scanner for mssql