opensource DBMS using a server-client setup. created and maintained by oracle. typically the database is backed up an a single .sql file

### MySQL clients
this is how you retrieve and/or modify data. Uses SQL (duh) depending on setup, can be internal only or can be internet facing

### MySQL Databases
well suited for apps such as dynamic websites where efficiency and speed are a priority. Often run as part of a LAMP setup (Linux, Apache, MySQL, PHP)  or LEMP setup (Linux, Nginx, MySQL, PHP) typically we store the content that PHP needs in the DB typically items include
- Headers
- Texts
- Meta tags
- Forms
- Customers
- Usernames
- Administrators
- Moderators
- Email addresses
- User information
- Permissions
- Passwords
- External/internal links
- links to files
- specific contents
- values
typically sensitive data should not be stored in plaintext but rather as a hash

### MySQL Commands
no commands covered here but noted that commands are how you interact with the database and you can use responses and error messages to learn more

### Default Configuration
Data Bases are a beast, if you want to go be a DB admin that's a thing you can do. going in depth is out of scope for this section so go set one up yourself play with it etc.

### Dangerous settings

| Setting            | Description                                                                                                 |
| ------------------ | ----------------------------------------------------------------------------------------------------------- |
| `user`             | Sets which user the MySQL service will run as                                                               |
| `password`         | sets the password for the MySQL user                                                                        |
| `admin_address`    | The IP address on which to listen for TCP/IP ocnnections on the administrative network interface            |
| `debug`            | This variable indicates the current debugging settings                                                      |
| `sql_warnings`     | This variable controls whether single-row INSERT statemnts produce an information string if warnings occur. |
| `secure_file_priv` | This variable is used to limit the effect of data import and export operations.                             |
noteworthy, the first three entries are made in plain text, if you get onto the server, you now own the database if you can read this file. debug and sql_warnings have to do with verbosity of errors
### Footprinting the Service

SQL servers should Ideally never be public facing...that said, quick temp fix to just make it work?
MySQL runs on port 3306
remember that scans can return false positives so confirm everything you find. When you're in and looking at the database pay close attention to the system schema and the information schema, they contain tables, info, and metadata necessary for management. System schema typically has more data associated with it. below are some MySQL commands

| Command                                            | Description                                                                                    |
| -------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| `mysql -u <username> -p<password> -h <ip-address>` | Connect to the MySQL server. There should NOT be a space between the -p flag, and the password |
| `show databases;`                                  | show all databeses                                                                             |
| `use <database>;`                                  | select one of the existing databases                                                           |
| `show tables;`                                     | show all available tables in the selected database                                             |
| `show columns from <table>;`                       | Show all columns in the selected table                                                         |
| `select * from <table>;`                           | show everything in the desired table                                                           |
| `select * from <table where <column> = "<string"`  | search for needed string in the desired table                                                  |
