Domain information refers to an organizations entire presence on the internet. This information is gathered passively  navigating as though we were customers/visitors. We can use third-party services to understand the company better, but first start with scrutinizing the main website and gathering all the important info you can. Remember this is where we focus on what do we see? and what do we not see?
### Online Presence
The first thing we will likely want to look at is the SSL certificate from the company's main website. this can help us find subdomains. Another source is [crt.sh](https://crt.sh), this is meant to ensure certificate transparency and to allow certificate verification. We can use this data to find subdomains.
##### Company Hosted Servers
We can use the data from crt.sh to find what is self-hosted and what is hosted by a third party (remember we need permission to attack third party hosting). the host command lets us do this.

After that we can gather osint with [shodan](https://shodan.io) 

After we find what is worth further investigating on [shodan](https://shodan.io) we can do further research by pulling dns records using dig/nslookup. Remember there are more than just DNS `A` Records and all of them may have something interesting for us
- `A` map IPv4 address to specific (sub)domain
- `AAAA` map IPv6 address to specific (sub)domain
- `MX` Shows us which mail server is responsible for managing the emails. 
- `NS` which name servers are used to resolve the FQDN to IP Address, most hosting providers use their own, making it easier to identify the hosting provider
- `TXT` typically used for verification keys and other security items. 