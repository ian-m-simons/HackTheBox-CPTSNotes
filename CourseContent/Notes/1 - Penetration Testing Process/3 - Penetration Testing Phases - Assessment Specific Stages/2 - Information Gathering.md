Information gathering is the most frequent and vital phase throughout the penetration testing process. We will return to it again and again throughout the engagement. Information gathering is the cornerstone of any penetration test. we can divide the way we gather information into four categories:
1. Open-source Intelligence 
2. Infrastructure Enumeration
3. Service Enumeration
4. Host Enumeration

All four categories are needed for each test. 
### Open-Source Intelligence (OSINT)
OSINT is a process for finding publicly available information on a target company or individuals that allows the identification of events, external and internal dependencies, and connections. You can sometimes find highly sensitive information such as passwords hashes, keys etc. in places like GitHub and other development platform if not set up correctly. StackOverflow is another great resource for OSINT
### Infrastructure Enumeration
here we use services such as DNS to create a map of the client's servers and hosts to develop an understanding of their infrastructure and how it is structured.
### Service Enumeration
here we want to identify what services we can interact with as well as their version, any other information they provide us, and if possible we want to identify the reason they are available. It is common for administrators to choose security gaps over patching vulnerable software/services etc
### Host Enumeration
here we examine every single host listed in the scoping document, find the OS, what services it uses as well as what version. If you're looking from inside the network, this is where most administrators get careless because they're not accessible from the internet ergo they are secure right? we are also looking for files, local services, scripts, applications, information and anything else worth grabbing that could be stored on the host.
### Pillaging
Pillaging is where we collect sensitive information locally on an already exploited host. We are going to do a lot of pillaging while we are going through this path, there will be plenty of practice.