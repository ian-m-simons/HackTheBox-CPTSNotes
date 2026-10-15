IMAP lets you use multiple email clients whereas pop3 does not. You can send multiple commands in succession, you don't have to wait for responses. IMAP also lets you sort emails into folders, it is also the reason you can have a sent folder. by default IMAP is unencrypted. Can also use IMAPS using TLS and typically port 993
### Default Configuration
IMAP and POP3 are both very deep, so we can't cover everything. it is recommended you install them yourself, play with them and break them. 
#### IMAP Commands 

| Command                         | Description                                                                                               |
| ------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `1 LOGIN username password`     | User's login                                                                                              |
| `1 LIST "" *`                   | Lists all directories                                                                                     |
| `1 CREATE "INBOX"`              | Creates a mailbox with a specified name (inbox in this case)                                              |
| `1 DELETE "INBOX"`              | Deletes a mailbox (inbox in this case)                                                                    |
| `1 RENAME "ToRead" "Important"` | Renames a mailbox                                                                                         |
| `1 LSUB "" *`                   | Returns a subset of names from the set of names that the User has declared as being active or subscribed. |
| `1 SELECT INBOX`                | Selects a mailbox so that messages in the mailbox can be accessed                                         |
| `1 UNSELECT INBOX`              | Exits the selected mailbox                                                                                |
| `1 FETCH <ID> all`              | Retrieves data associated with a message in the mailbox                                                   |
| `1 CLOSE`                       | removes all messages with the Deleted flag set                                                            |
| `1 LOGOUT`                      | Closes the connection with the IMAP server                                                                |
#### POP3 Commands

| Command         | Description                                               |
| --------------- | --------------------------------------------------------- |
| `USER username` | Identifies the user                                       |
| `PASS password` | Authentication of the user using its password             |
| `STAT`          | Requests the number of saved emails from the server       |
| `LIST`          | Requests the server the number and size of all emails     |
| `RETR id`       | Requests the server to deliver the requested email by ID. |
| `DELE id`       | Requests the server to delete the requested email by ID   |
| `CAPA`          | Requests the server to display the server capabilities    |
| `RSET`          | Requests the server to reset the transmitted information  |
| `QUIT`          | Closes the connection with the POP3 server                |
### Dangerous Settings

| Setting                 | Description                                                                              |
| ----------------------- | ---------------------------------------------------------------------------------------- |
| auth_debug              | Enables all authentication debug logging                                                 |
| auth_debug_passwords    | This setting adjusts log verbosity, the submitted passwords, and the scheme gets logged. |
| auth_verbose            | Logs unsuccessful authentication attempts and their reasons                              |
| auth_verbose_passwords  | Passwords used for authentication are lagged and can also be truncated                   |
| auth_anonymous_username | This specifies the username to be used when logging in with the ANONYMOUS SASL mechanism |
### Footprinting the service

POP3 port 110 POP3S port 995 IMAP port 143 IMAPS port 993. higher ports are encrypted using TLS. Nmap by default give us the common name, displayed capabilities. with curl we can use the -v flag to see what version of TLS is used and even further SSL certificate data and the banner. to interact with the service you would use openssl or ncat depending on if it is encrypted or not.