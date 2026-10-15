Simple mail transfer protocol is for sending emails. works client to server or server to server. SMTP is plainetext by default, if using starttls it goes over port 587 typically. Typcially when people say SMTP nowadays they mean ESMTP (Extended SMTP)

### Default Configuration
The below commands are useful for communicating with the SMTP server

| Command      | Description                                                                                         |
| ------------ | --------------------------------------------------------------------------------------------------- |
| `AUTH PLAIN` | AUTH is a service extension used to authenticate the client.                                        |
| `HELO`       | The client logs in with its computer name and thus starts the session                               |
| `MAIL FROM`  | The client names the email sender                                                                   |
| `RCPT TO`    | The client names the email recipient                                                                |
| `DATA`       | The client initiates the transmission of the email                                                  |
| `RSET`       | The client aborts the initiated transmission but keeps theconnection between the client and server. |
| `VRFY`       | The client checks if a mailbox is available for message transfer                                    |
| `EXPN`       | The client also checks if a mailbox is available for messaging with this command                    |
| `NOOP`       | The client requests a response from the server to prevent disconnection due to time-out             |
| `QUIT`       | The client terminates the session.                                                                  |
you can use telnet to interact with this service 

### Dangerous Settings

open Relay configuration basically send to a relay then to target setting is below

```
mynetworks = 0.0.0.0/0
```
this allows all inbound addresses

### Footprinting the Service

Nmap default scripts will do some footprinting for you, it utilizes the `HELO` this lists all available commands. The smtp-open-relay script will identify if a server is an open-relay