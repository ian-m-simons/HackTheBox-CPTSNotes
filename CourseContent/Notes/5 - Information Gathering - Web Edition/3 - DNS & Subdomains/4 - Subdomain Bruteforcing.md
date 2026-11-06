there are 4 steps to subdomain bruteforcing

1. `Wordlist Selection`: select a wordlist, generally speaking you have 3 categories: `General-purpose`, `Targeted`, and `Custom`
2. `Iteration and Querying`: A script or tool iterates through the wordlist, appending each word or phrase to the main domain to create potential subdomains
3. `DNS lookup`: A DNS query is performed for each potential subdomain to check if it resolves to an IP address. This is typically done using the A or AAA record type
4. `Filtering and Validation`: if a subdomain resolves successfully, it's added to a list of valid subdomains. Further validation steps might be taken to confirm the subdomain's existence and functionality
common tools include 

| Tool          | Description                                                                                                                    |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `dnsenum`     | Comprehensive DNS enumeration tool that supports dictionary and brute-force attacks for discovering subdomains                 |
| `fierce`      | User-friendly tool for recursive subdomain discovery, featuring wildcard detection and an easy-to-use interface                |
| `dnsrecon`    | Versatile tool that combines multiple DNS reconnaissance techniques and offers customizable output formats                     |
| `amass`       | Actively maintained tool focused on subdomain discovery, known for its integration with other tools and extensive data sources |
| `assetfinder` | Simple yet effective tool for finding subdomains using various techniques, ideal for quick and lightweight scans               |
| `puredns`     | Powerful and flexible DNS brute-forcing tool, capable of resolving and filtering results effectively                           |
### [DNSEnum](../../../TTPs%20and%20Tools/Tools/Service%20Enumeration/DNSEnum.md)
versatile widely used commandline tool written in Perl. Key functions include:
- `DNS Record Enumeration:` can retrieve various DNS records including A, AAAA, NS, MX, and TXT records, providing a comprehensive overview of the target's DNS configuration.
- `Zone Transfer Attempts`: The tool automatically attempts zone transfers from discovered name servers. while most servers are configured to prevent unauthorized zone transfers a successful attempt can reveal a treasure trove of DNS information
- `Subdomain Brute-Forcing`: supports brute-force enumeration of subdomains using a wordlist. This involves systematically testing potential subdomain names against the target domain to identify valid ones.
- `Google Scriping`: The tool can scripe Google search results to find additional subdomains that might not be listed in DNS records directly
- `Reverse Lookup`: can perform reverse DNS lookups to identify domains associated with a given IP address, potentially revealing other websites hosted on the same server
- `WHOIS lookups`: the tool can also perform WHOIS queries to agther information about domain ownership and registration details