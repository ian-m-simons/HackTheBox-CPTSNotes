it is important that we develop a consistent methodology so we don't forget things. We will go over a static enumeration methodology which is nested 6 layers deep and contains the following 3 different levels
- Infrastructure-based enumeration
- Host-based enumeration
- OS-based enumeration
![image.jpg](CourseContent/Images/FootPrinting/enum-method33.jpg)
note that the above image covers general categories, not a full list of all components to search for. the layers are designed as follows

| Layer                  | Description                                                                                           | Information Categories                                                                               |
| ---------------------- | ----------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| 1. Internet Presence   | Identification of internet presence and externally accessible infrastructure.                         | Domains, subdomains, vHosts, ASN, Netblocks, IP Addresses, Cloud Instances, Security Measures        |
| 2. Gateway             | Identify the possible security measures to protect the company's external and internal infrastructure | Firewalls, DMZ, IDS/IPS, EDR, Proxies, NAC, Network Segmentation, VPN, Cloudflare                    |
| 3. Accessible Services | Identify accessible interfaces and services that are hosted externally or internally                  | Service Type, Functionality, Configuration, Port, Version, Interface                                 |
| 4. Processes           | Identify the internal processes, sources, and destinations, associated with the services.             | PID, Processed Data, Tasks, Source, Destination                                                      |
| 5. Privileges          | Identification of internal permissions and privileges to the accessible services.                     | Groups, Users, Permissions, Restrictions, Environment                                                |
| 6. OS Setup            | Identification of the internal components and systems setup.                                          | OS Type, Patch Level, Network config, OS environment, configuration files, sensitive private files.  |
if we look at the below picture, assume that all the squares are security gaps we can get through, but we can't cross through any of the lines, our job is to follow through this labyrinth to get to the center
![img2.jpg](CourseContent/Images/FootPrinting/pentest-labyrinth.jpg)
While not every Gaps are a way in, there is nearly a 99% chance a way in exists. Even if we don't find it we can't say with 100% certainty that there are no more vulnerabilities. 
the remainder of this section walks through this model in a mock pentest fashion
### Layer No.1: Internet Presence
in this layer we focus on finding targets if the scope allows. we are trying to find domains, subdomains, netblocks, and many other components and information that present the presence of the company and its infrastructure on the internet.
`The goal of this layer is to identify all possible target systems and interfaces that can be tested.`
### Layer No.2: Gateway
here we are trying to understand the interface of the reachable target. We will cover this in more detail in a later module for now
`The goal of this layer is to understand what we are dealing with and what we have to watch out for`
### Layer No.3: Accessible Services
here we examine each destination and all the services it offers. Remember each service was installed for a reason. we need to know how these services work and learn to understand them
`The goal of this layer is to understand the reason and functionality of the target system, and gain the necessary knowledge to communicate with it  and exploit it for our purpose effectively`
### Layer No.4: Processes
processes occur every time a function or command is executed. tasks have at least one source and one target, and data is being processed, it is either supplied by the system or the user. 
`The goal of this layer is to understand these factors and identify the dependencies between thme`
### Layer No.5: Privileges
services run through a user in a group, with premissions and privileges defined there by the admin or system. It is super common that these permissions are set wrong in AD especially
`The goal of this layer is to identify and understand what is possible and what is not possible with the privileges we have`
### Layer No.6: OS Setup
here we collect information about the actual OS and its setup. This gives us an overview of the internal security and skills and capabilities of the admin/security team
`The goal of this layer is to see how the administrators manage the systems and what sensitive internal information we can glean from them.`
### Enumeration Methodology in Practice
remember, a methodology is a summary of a systematic procedures. How we identify components and information changes dynamically. The methodology stays the same but the techniques vary over time etc.