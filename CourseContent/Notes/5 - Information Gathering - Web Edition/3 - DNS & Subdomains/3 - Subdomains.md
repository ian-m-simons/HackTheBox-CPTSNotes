subdomains are extensions of the main domain often created to organize and separate different sections or functionalities of a website.
### Why are subdomains important for web reconnaissance?
often host valuable information and resources not linked from the main website for example:
- `Development and Staging Environments`: Companies often use subdomains to test new features or updates before deploying them to the main site. Due to relaxed security measures, these environments sometimes contain vulnerabilities or expose sensitive information.
- `Hidden Login Portals`: Subdomains might host administrative panels or other login pages that are not meant to be publicly accessible. Attackers seeking unauthorized access can find these as attractive targets.
- `Legacy Applications`: Older, forgotten web applications might reside on subdomains, potentially containing outdated software with known vulnerabilities
- `Sensitive Information`: Subdomains can inadvertently expose confidential documents, internal data, or configuration files that could be valuable to attackers.

### Subdomain Enumeration

##### 1. Active Subdomain Enumeration
Direct interaction with domain's DNS servers. DNS zone transfer can leak a complete list of subdomains (though typically blocked nowadays)
Typically need brute-force enumeration with `dnsenum`, `ffuf`, and/or `gobuster`
##### 2. Passive Subdomain Enumeration
enumeration without direct interaction for example Certificate transparency logs, search engines etc

both passive and active have advantages and disadvantages, use both as needed