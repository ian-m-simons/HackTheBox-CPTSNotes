the Pre-Engagement is the preparation stage where you work with the client to determine scope, targets, and create contracts etc. It consists of three essential components 
1. scoping questionnaire
2. Pre-engagement meeting
3. kick-off meeting

Before we can do any of this we need to complete Non-Disclosure agreements. Generally speaking, there are three types of NDAs

| Type           | Description                                                                                                                                                                                 |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Unilateral NDA | This type of NDA obligates only one party to maintain confidentiality and allows the other party to share the information received with third parties                                       |
| Bilateral NDA  | In this type, both parties are obligated to keep the resulting and acquired information confidential. This is the most common type of NDA that protects the work of penetration testers.    |
| Multilater NDA | this is a commitment to confidentiality by more than two parties. If we conduct a penetration test for a cooperative network, all parties responsible and involved must sign this document. |
Remember that who we are working with at a company matters, a helpdesk employee can't contract a penetration test, that is likely an attempt to harm the company. Generally we can expect requests to come from:
- Chief Executive Officer (CEO)
- Chief Technical Office (CTO)
- Chief Information Security Officer (CISO)
- Chief Security Officer (CSO)
- Chief Risk Officer (CRO)
- Chief Information Officer (CIO)
- VP of Internal Audit
- Audit Manager
- VP or Director of IT/IS
this is the stage where all documentation must be signed by all relevant parties. A general document timeline is below

| Document                                                       | Timing for Creation                             |
| -------------------------------------------------------------- | ----------------------------------------------- |
| 1. Non-Disclosure Agreement (NDA)                              | After Initial Contact                           |
| 2. Scoping Questionnaire                                       | Before Pre-engagement meeting                   |
| 3. Scoping Document                                            | During the Pre-engagement meeting               |
| 4. Penetration Testing Proposal (contract/scope of work (SOW)) | During the Pre-engagement meeting               |
| 5. Rules of Engagement (RoE)                                   | Before the kick-off meeting                     |
| 6. Contractors agreement (physical assessments)                | Before the Kick-off meeting                     |
| 7. Reports                                                     | during and after the conducted penetration Test |
### Scoping Questionnarie
typically sent to help us better understand the services the client is seeking and should clearly explain our services, likely asks them to choose one or more from the following list
- [ ] Internal Vulnerability Assessment
- [ ] Internal Penetration Test
- [ ] Wireless Security Assessment
- [ ] Physical Security Assessment
- [ ] Red Team Assessment
- [ ] External Vulnerability Assessment
- [ ] External Penetration Test
- [ ] Application Security Assessment
- [ ] Social Engineering Assessment
- [ ] Web Application Security Assessment
this is where we get details about how deep to go. Are we just doing phishing? or are we vishing as well, how stealthy are we aiming to be? etc. In this phase you also need to identify the client name address, and key personnel contact information. some critical items to identify here include:
- How many expected live hosts?
- How many IPs/CIDR ranges in scope?
- How many Domains/subdomains are in scope?
- How many wireless SSIDs are in scope?
- How many web/mobile applications? If testing is authenticated, how many roles (standard users, admin etc)
- For a phishing assessment, how many users will be targeted? will the client provide a list or will we be required to gather this list via osint?
- If the client is requesting a Physical Assessment, how many locations? If multiple sites are in scope, are they geographically dispersed?
- What is the objective of the red team assessment? are any activities (such as phishing or physical security attacks) out of scope?
- is a separate Active Directory Security Assessment desired?
- Will network testing be conducted from an anonymous user on the network? or a standard domain user?
- Do we need to bypass NAC
Finally we need info about disclosure and evasiveness
- blackbox, greybox, or whitebox?
- evasive or hybrid-evasive?
### Pre-Engagement meeting
During this phase we will write up our Penetration Testing Proposal also known as the contract or scope/statement of work (SoW)
Contract checklist
##### Contract - Checklist

| checkpoint                           | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [ ] NDA                              | Non-Disclosure Agreement (NDA) refers to a secrecy contract between the client and the contractor regarding all written or verbal information concerning an order/project. The contractor agrees to treat all confidential information brought to its attention as strictly confidential, even after the order/project is completed. Furthermore, any exceptions to confidentiality, the transferability of rights and obligations, and contractual penalties shall be stipulated in the agreement. The NDA should be signed before the kick-off meeting or at the latest during the meeting before any information is discussed in detail. |
| [ ] Goals                            | Goals are milestones that must be achieved during the order/project. In this process, goal setting is started with the significant goals and continued with fine-grained and small ones.                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| [ ] Scope                            | The individual components to be tested are discussed and defined. These may include domains, IP ranges, individual hosts, specific accounts, security systems, etc. Our customers may expect us to find out one or the other point by ourselves. However, the legal basis for testing the individual components has the highest priority here.                                                                                                                                                                                                                                                                                              |
| [ ] Penetration Testing Type         | When choosing the type of penetration test, we present the individual options and explain the advantages and disadvantages. Since we already know the goals and scope of our customers, we can and should also make a recommendation on what we advise and justify our recommendation accordingly. Which type is used in the end is the client's decision.                                                                                                                                                                                                                                                                                  |
| [ ] Methodologies                    | Examples: OSSTMM, OWASP, automated and manual unauthenticated analysis of the internal and external network components, vulnerability assessments of network components and web applications, vulnerability threat vectorization, verification and exploitation, and exploit development to facilitate evasion techniques.                                                                                                                                                                                                                                                                                                                  |
| [ ] Penetration Testing Locations    | External: Remote (via secure VPN) and/or Internal: Internal or Remote (via secure VPN)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| [ ] Time Estimation                  | For the time estimation, we need the start and end dates for the penetration test. This provides a precise time window to perform the test and helps us plan our procedure. It is also vital to explicitly determine the duration of the time windows for each phase of the attack, such as Exploitation, Post-Exploitation, and Lateral Movement. These can be carried out during or outside regular working hours. When testing outside regular working hours, the focus is more on the security solutions and systems that should withstand our attacks.                                                                                 |
| [ ] Third Parties                    | For the third parties, it must be determined via which third-party providers our customer obtains services. These can be cloud providers, ISPs, and other hosting providers. Our client must obtain written consent from these providers describing that they agree and are aware that certain parts of their service will be subject to a simulated hacking attack. It is also highly advisable to require the contractor to forward the third-party permission sent to us so that we have actual confirmation that this permission has indeed been obtained.                                                                              |
| [ ] Evasive Testing                  | Evasive testing is the test of evading and passing security traffic and security systems in the customer's infrastructure. We look for techniques that allow us to find out information about the internal components and attack them. It depends on whether our contractor wants us to use such techniques or not.                                                                                                                                                                                                                                                                                                                         |
| [ ] Risks                            | We must also inform our client about the risks involved in the tests and the possible consequences. Based on the risks and their potential severity, we can then set the limitations together and take certain precautions.                                                                                                                                                                                                                                                                                                                                                                                                                 |
| [ ] Scope Limitations & Restrictions | It is also essential to determine which servers, workstations, or other network components are essential for the client's proper functioning and its customers. We will have to avoid these and must not influence them any further, as this could lead to critical technical errors that could also affect our client's customers in production.                                                                                                                                                                                                                                                                                           |
| [ ] Information Handilng             | HIPAA, PCI, HITRUST, FISMA/NIST, etc.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| [ ] Contact Information              | For the contact information, we need to create a list of each person's name, title, job title, e-mail address, phone number, office phone number, and an escalation priority order.                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| [ ] Lines of Communication           | It should also be documented which communication channels are used to exchange information between the customer and us. This may involve e-mail correspondence, telephone calls, or personal meetings.                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| [ ] Reporting                        | Apart from the report's structure, any customer-specific requirements the report should contain are also discussed. In addition, we clarify how the reporting is to take place and whether a presentation of the results is desired.                                                                                                                                                                                                                                                                                                                                                                                                        |
| [ ] Payment Terms                    | Finally, prices and the terms of payment are explained.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
The most important part here, is aligning our focus with the clients desires. We wouldn't serve a medium rare steak to someone who asked for it well done even though the medium rare steak is objectively better. 

##### Rules of Engagement - Checklist

| Checkpoint                                   | Contents                                                                                              |
| -------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| [ ] Introduction                             | Description of this document.                                                                         |
| [ ] Contractor                               | Company name, Contractor full name, job title.                                                        |
| [ ] Penetration Testers                      | Company name, pentesters full name.                                                                   |
| [ ] Contact Information                      | Mailing addresses, e-mail addresses, and phone numbers of all client parties and penetration testers. |
| [ ] Purpose                                  | Description of the purpose for the conducted penetration test.                                        |
| [ ] Goals                                    | Description of the goals that should be achieved with the penetration test.                           |
| [ ] Scope                                    | All IPs, domain names, URLs, or CIDR ranges.                                                          |
| [ ] Lines of Communication                   | Online conferences, phone calls, face-to-face meetings, or email                                      |
| [ ] Time Estimation                          | Start and End dates                                                                                   |
| [ ] Time of the Day to Test                  | Times of the day to test                                                                              |
| [ ] Penetration Testing Type                 | External/Internal Penetration Test/Vulnerability Assessments/Social Engineering.                      |
| [ ] Penetration Testing Locations            | Description of how the connection to the client network is established                                |
| [ ] Methodologies                            | OSSTMM, PTES, OWASP, etc                                                                              |
| [ ] Objectives/Flags                         | Users, Specific files, specific information etc.                                                      |
| [ ] Evidence Handling                        | Encryption, secure protocols                                                                          |
| [ ] System Backups                           | Config files, databases, etc                                                                          |
| [ ] Information Handling                     | Strong data encryption                                                                                |
| [ ] Incident Handling and Reporting          | Cases for contact, pentest interruptions, type of reports                                             |
| [ ] Status Meetings                          | Frequency of meetings, dates, times, included parties                                                 |
| [ ] Reporting                                | Type, target readers, focus                                                                           |
| [ ] Retesting                                | Start and end dates                                                                                   |
| [ ] disclaimers and Limitations of Liability | System damage, data loss                                                                              |
| [ ] Permission to Test                       |  Signed contract, contractors agreement                                                               |
### Kick-Off Meeting
This is where we go over the nature of a penetration test, as well as identify findings which will pause the penetration test and cause us to reach out to our PoC ie RCE in public facing server, illegal activity on internal asset, evidence of an external threat actor/prior breach. We also need to explain the risks associated for example lots of log entries alarms in security software accidentally locking out users. We need to tell customers to contact us if the penetration test negatively impacts their network. Remember that most people you will interact with are not technical, for that reason we need to make sure even the CEO who has been working since before computers existed can understand what is going on. Giving good explanations also will likely buy us good will and more latitude. As the call goes on you should be able to get an idea of how familiar the client is with penetration testing and you should adapt your pitch appropriately
### Contractors Agreement
The contractors Agreement is our get out of jail free card. This is particularly important for physical assessments as employees who don't know they're facing a penetration test are (hopefully) apt to call the cops.
##### Contractors Agreement - Checklist for Physical Assessments
- [ ] Introduction
- [ ] Contractor
- [ ] Purpose
- [ ] Goal
- [ ] Penetration Testers
- [ ] Contact Information
- [ ] Physical Addresses
- [ ] Building Name
- [ ] Floors
- [ ] Physical Room Identifiers
- [ ] Physical Components
- [ ] Timeline
- [ ] Notarization
- [ ] Permission to Test
### Setting up
Only after everything above has been taken care start preparing for our penetration test, ie building VMs VPSs etc. 