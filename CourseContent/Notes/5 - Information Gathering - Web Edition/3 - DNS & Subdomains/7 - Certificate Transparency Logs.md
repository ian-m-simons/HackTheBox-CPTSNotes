Certificate Transparency logs that are public, append-only ledgers that record the issuance of SSL/TLS certificates. Independent organizations (not CA's) maintain these logs and they are open for anyone to inspect. Transparency logs serve several crucial purposes:
- `Early Detection of Rogue Certificates`: CT logs allow quick identification of suspicious or misissued certificates. A rogue certificate is an unauthorized or fraudulent digital certificate issued by a trusted certificate authority. Detecting these early allows for swift action to revoke the certificates before they can be used for malicious purposes
- `Accountability for Certificate Authorities`: CT logs hold CAs accountable for their issuance practices. 
- `Strengthening the Web PKI (public key infrastructure`: The web PKI is the trust system underpinning secure online communication. CT logs help to enhance the security and integrity of the WEB PKI by allowinsg public oversight and verification of certificates 
### CT Logs and Web Recon
CT Logs give you a list of every domain and subdomain that was issued a certificate for this target. in addition they can show old or expired certificates which may reveal other subdomains etc with outdated software configurations etc 
### Searching CT Logs
there are two popular options 

| Tool   | Key Features                                                                                                    | Use Cases                                                                                                | Pros                                             | Cons                                        |
| ------ | --------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | ------------------------------------------------ | ------------------------------------------- |
| crt.sh | User-friendly web interface, simple search by domain, displays certificate details, SAN entries                 | Quick and easy searches, identifying subdomains, checking certificate issuance history                   | Free, easy to use, no registration required      | Limited filtering and analysis options      |
| Censys | Powerful search engine for internet-connected devices, advanced filtering by domain, IP, certificate attributes | In-depth analysis of certificates, identifying misconfigurations, finding related certificates and hosts | Extensive data and filtering options, API access | Requires registration (free tier available) |
### crt.sh lookup 
use the API to make things faster and run them from your terminal
```
n00blyfe@htb$ curl -s "https://crt.sh/json?q=facebook.com"
```