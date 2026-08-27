A Penetetration Test  (PenTest) is an organized, targeted, and authorized attack attempt to test IT infrastructure and its defenders to determine their susceptibility to IT security vulnerabilities. 
### Risk Management
the main goal of IT security risk management is to identify, evaluate, and mitigate any potential risks that could damage the CIA of an organizations Information systems and data, and reduce the overall risk to an acceptable level. Inherent risk is the level of risk that is present even when the appropriate security controls are in place. 
Our job is to:
- identify vulnerabilities
- provide detailed reproduction steps
- provide appropriate remediation recommendations
we do NOT fix it for them, or monitor the IT infrastructure. We provide a snapshot of the security status at the time we perform the test. A statement to this should be reflected in our penetration test report deliverable.
### Vulnerability Assessments
Vulnerability analysis is a generic term covering vulnerability & security assessments, and penetration tests. Vulnerability Assessments are performed purely using automated tools. A pentest is a mix of automated and manual testing/validation and is preformed after extensive, in most cases, manual information gathering. None of this (vulnerability & security assessment or pentesting) can be performed without mutual agreement between the contracting company and the organization employing the pentester. A successful pentest requires considerable organization and preparation. Usually employees will not be warned of a penetration test, but sometimes for data privacy reasons they will be warned.
### Testing methods
every pentest can be performed from two different perspectives, external and internal.
##### External Penetration Test
Performed from an external perspective or anonymous internet user. can be performed from our host using a VPN or from a VPS. some clients will ask for a stealthy or hybrid approach where we try to avoid triggering alarms or start stealthy then gradually get louder to test their detection capabilities. the goal is still attack external-facing hosts to compromise sensitive data or gain access to the internal network.
##### Internal Penetration Test
performed from within the corporate network. May be executed after successful external pentest or start from an assumed breach. Sometimes it may require physical presence if accessing isolated systems. 
### Types of Penetration Testing
type of test is based on how much information is made available to us

| Type           | Information provided                                                                                                                                                                                                             |
| :------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Blackbox       | Minimal, only the essential information, such as IP addresses and domains are provided                                                                                                                                           |
| Greybox        | Extended. In this case we are provided with additional information such as specific URLs, hostnames, subnets, and similar information                                                                                            |
| Whitebox       | Maximum. Everything is disclosed. This gives us an internal view of the entire structure which allows us to prepare an attack using internal information. We may be given detailed configs, admin creds, web app source code etc |
| Red-Teaming    | May include physical testing and social engineering, among other things. Can be combined with any of the above types.                                                                                                            |
| Purple-Teaming | It can be combined with any of the above types. However it focuses on working closely with defenders                                                                                                                             |
The less information we are given, the longer and more complex the approach we will have to take. 
### Types of Testing Environments
need to consider what is being tested. Categories include:
- Network
- Web app
- Mobile
- API
- Thick Clients
- IoT
- Cloud
- Source Code
- Physical Security
- Employees
- Hosts
- Servers
- Security Policies
- Firewalls
- IDS/IPS
These categories can be mixed and matched depending on the goals and scope.