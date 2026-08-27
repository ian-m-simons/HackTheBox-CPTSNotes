In this stage we want to test how far we can move manually in the entire network and what vulnerabilities we can find from the internal perspective that might be exploited. This will take us back through the following stages:
1. Pivoting
2. Evasive Testing
3. Information Gathering
4. Vulnerability Assessment
5. (Privilege) Exploitation
6. Post-Exploitation
Sometimes Lateral movement is our only post-exploitation option
### Pivoting
Systems you break into won't typically have tools to enumerate the internal network. Sometimes we can use the exploited host as a proxy and perform all the scans from our attack machine. This lets us get deeper into the network even though it is not routable. it is also known as pivoting or tunneling. the goal of pivoting is to access inaccessible systems via an intermediary system.
### Evasive Testing
This is the stage where we really need to consider the evasive testing scope of the assessment, are we supposed to be stealthy or not? If so we need to figure out what is trying to catch us (IPS/IDS, EDR, Threat Monitoring etc) how it works, and then what strategies we can use to avoid it.
### Information Gathering
Again we need to gather more information from our new point of view, Enumeration is key
### Vulnerability Assessment
Goes hand in hand with information gathering. That said, for more errors occur here than when on infrastructure which is facing the internet. Groups and rights come into play here and compromising a user may yield more results than normal. 
### (Privilege) Exploitation
Here we use the privilege we've gained to access other systems and/or accounts.
### Post-Exploitation
after we move laterally we perform our post-exploitation steps again. finally we are ready to move on to the Proof-of-Concept to show off our hard work and help our client. 