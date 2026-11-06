vhostsThis is how you host multiple websites on a single web server

### How Virtual Hosts Work: Understanding VHosts and Subdomains

Sites are differentiated using the `HTT Host` header. the big difference between `VHosts` and `subdomains` is their relationship to the `Domain Name System (DNS)` and the web server's configuration
- `subdomains`: these are extensions of a main domain name. Subdomains typically have their own DNS records, pointing to either the same IP address as the main domain or a different one. They can be used to organize different sections or services of a website
- `Virtual Hosts (VHosts)`: Virtual hosts are configurations within a web server that allow multiple websites or applications to be hosted on a single server. They can be associated with top-level domains, or subdomains. Each virtual host can have its own separate configuration, enabling precise control over how requests are handled.
If a `VHost` does not have a DNS record you can getwto it by modifying your hosts file to map to it. `VHost fuzzing` is a technique to discover public and non-public subdomains and `VHosts` by testing various hostnames against a known IP address. 

### Server VHost Lookup

1. `Browser Requests a Website`: When you enter a domain name into your browser, it initiates an HTTP request to the web server associated with the domain's IP address
2. `Host Header Reveals the Domain`: The browser includes the domain name in the request's Host header, which acts as a label to inform the web server which website is being requested. 
3. `Web Server Determines the Virtual Host`: The web server receives the request, examines the Host header, and consults its virtual host configuration to find a matching entry for the requested domain name
4. `Serving the Right Content:` Upon identifying the correct virtual host configuration, the web server retrieves the corresponding files and resources associated with that website from its document root and sends them back to the browser as the HTTP response. 
### Types of Virtual Hosting

1. `Name-Based Virtual Hosting` just uses HTTP HOST Header, most common and flexible, but requires support from the web server and can have TLS limitations
2. `IP-Based Virtual Hosting`: unique IP for each website, IP is then used to determine which website to serve. doesn't use host header, requires multiple IP's which is more expensive and less scalable
3. `Port-Based Virtual Hosting` Different websites are associated with different ports on the same IP address. not as common or user friendly as `name-based virtual hosting`, and might require users to specify the port number in the URL but only requires a single IP
### Virtual Host Discover Tools
multiple tools exist for finding virtual hosts

| Tool          | Description                                                                                                      | Features                                                        |
| ------------- | ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| `gobuster`    | A multi-purpose tool often used for directory/file brute-forcing, but also effective for virtual host discovery. | Fast, supports multiple HTTP methods, can use custom wordlists. |
| `Feroxbuster` | Similar to Gobuster, but with a Rust-based implementation, known for its speed and flexibility                   | Supports recursion, wildcard discovery, and various filters.    |
| `ffuf`        | another fast eb fuzzer that can be used for virtual host discovery by fuzzing the Host header                    | Customizable wordlists input and filtering options              |

### Gobuster

to enumerate VHOSTS with gobuster run the following
```
n00blyfe@htb$ gobuster vhost -u http://inlanefreight.htb:81 -w /usr/share/seclists/Discover/DNS/subdomains-top1million-110000.txt --append-domain
```

### FFUF

syntax for virtual host fuzzing 
```
n00blyfe@htb$ ffuf -u http://<target IP> -H "Header: FUZZ.inlanefreight.htb" -u /usr/share/wordlist/seclists/Discovery/DNS/subdomains.txt -ac
```