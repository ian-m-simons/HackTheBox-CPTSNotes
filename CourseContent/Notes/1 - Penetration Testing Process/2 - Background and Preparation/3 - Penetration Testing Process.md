The penetration testing process is defined by successive steps and events performed by the penetration tester to find a path to the predefined objective. Processes describe sequences that lead to a desired result. they do not follow a fixed recipe
### Penetration Testing Stages
stages allow the individual steps and approaches to be flexible, varied, and to adapt to the results and information we receive. 
![Stages](Images/PenetrationTestingProcess/PT-PRocess.jpg)
##### Pre-engagement
educate the client and adjusting the contract. Define the scope and document it. At a minimum complete:
- Non-Disclosure Agreement (NDA)
- Goals
- Scope
- Time Estimation
- Rules of Engagement
##### Information Gathering
how do we gather information about the necessary components? we use the information we find to locate gaps and potential foot holds
##### Vulnerability Assessment
analyze results from information gathering. Look for known vulnerabilities that can serve as possible attack vectors. Goal is to determine the therat level and susceptibility of a company's network infrastructure to cybe-attacks
##### Exploitation
use results from previous stages to test our attacks, and execute them against the target systems
##### Post-Exploitation
we have gained initial access and ensured persistent access we now want to escalate our privileges and hunt for sensitive data (pillaging) or perform lateral movement
##### Lateral Movement
moving within an entirnal network to access additional hosts at the same or higher privilege levels. 
##### Proof of Concept
document, step-by-step, what we did to achieve compromise. Should paint a clear picture of how each vulnerability fits in and help prioritize remediation efforts. If feasible, create scripts to automate the steps we took to assist our client in reproducing our findings. 
##### Post-Engagement
Prepare Detailed documentation for both the administrators and client company management. clean up all traces of our actions on all hosts and servers. create deliverables for client and hold report walkthrough meeting. archive testing data per contractual obligations and company policy. 
### Importance
Learn these procedures, its the basis for all our technical engagements. below is a stage and summary description for a website penetration test

| Stage                       | Description                                                                                                                                                                                                                                                                                |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1. Pre-engagement           | The first step is to create all the necessary documents in the pre-engagement phase, discuss the assessment objectives, and clarify any questions.                                                                                                                                         |
| 2. Information Gathering    | Once the pre-engagement activities are complete, we investigate the company's existing website we have beenassigned to assess. We identify the technologies in use and learn how the web application functions.                                                                            |
| 3. Vulnerability Assessment | With this information, we can look for known vulnerabilities and investigate questionable features that may allow for unintended actions.                                                                                                                                                  |
| 4. Exploitation             | Once we have found potential vulnerabilities, we prepare our exploit code, tools, and environment and test the webserver for these potential vulnerabilites.                                                                                                                               |
| 5. Post-Exploitation        | Once we have successfully exploited the target, we jump into information gathering and examine the webserver from the inside. If we find sensitive information during this stage, we try to escalate our privileges (depending on the system and configurations).                          |
| 6. Lateral Movement         | If other servers and hosts in the internal network are in scope, we then try to move through the network and access other hosts and servers using the information we have gathered.                                                                                                        |
| 7. Proof-of-Concept         | We create a proof-of-concept that proves that these vulnerabilities exist and potentially even automate the individual steps that trigger these vulnerabilities.                                                                                                                           |
| 8. Post-Engagement          | Finally, the documentation is completed and presented to our client as a formal report deliverable. Afterward, we may hold a report walkthrough meeting to clarify anything about our testing or results and provide any needed support to personnel tasked with remediating our findings. |