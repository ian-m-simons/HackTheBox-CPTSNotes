used for DNS, IP address blocks, and autonomous systems. kinda like a giant phonebook for the internet. Typical WHOIS record contains the following
- Domain name: the domain name itself
- Registrar: The company where the domain was registered (GoDaddy, Namecheap)
- Registrant Contact: The person or organization that registered the domain
- Administrative contact: the person responsible for managing the domain
- Technical contact; the person handling the technical issues related to the domain
- Creation and Expiration Dates: when the domain was registered and when its set to expire
- Name Servers: Servers that translate the domain name into an IP address
### History of WHOIS
developed at stanford in the 70's when ARPANET was still a thing. 

### Why WHOIS Matters for Web Recon
typically offers lots of interesting information including:
- Identifying Key Personnel: WHOIS records often reveal the names, email addresses, and phone numbers of individuals responsible for managing the domain. This information can be leveraged for social engineering attacks, or to identify potential phishing targets
- Discovering Network Infrastructure: Technical details like name servers and IP addresses provide clues about the target's network infrastructure. This can help penetration testers identify potential entry points or misconfigurations
- Historical Data Analysis: Accessing historical WHOIS records through services like [WhoisFreaks](https://whoisfreaks.com) can reveal changes in ownership, contact information, or technical details over time. This can be useful for tracking the evolution of the target's digital presence. 