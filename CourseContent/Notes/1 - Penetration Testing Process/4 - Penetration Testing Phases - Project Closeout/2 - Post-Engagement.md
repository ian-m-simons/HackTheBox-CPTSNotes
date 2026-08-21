Just like there's a ton to do in the pre-engagement, there's a ton to do post-engagement before you can fully close it out
### Cleanup
Here we go through and clean up after ourselves. We delete tools/scripts, revert any changes we made, delete accounts etc. If we are unable to cleanup ourselves, then we need to notify the client so they can clean up. We should also document all changes we made which need to be cleaned up so that the client knows they came from us in case they receive alerts etc.
### Documentation and Reporting
Before we give the stop signal to get our team out completely out of the network, we need to ensure that we have adequate documentation for all findings. We should include screenshots, command outputs etc. Ensure that you delet any PII or other potentially sensitive/incriminating data you found along the way. Our report should consist of:
- A full attack chain detailing steps taken to achieve compromise
- A strong executive summary that a non-technical audience can understand
- Detailed findings specific to the client's environment that include risk rating, finding impact, remediation recommendations, and high-quality external references related to the issue.
- Adequate steps to reproduce each finding so the team responsible for remediation can understand and test the issue while implementing the remediation
- Short, medium, and long-term recommendations specific to the environment
- Appendices which include information such as the target scope, OSINT data, password cracking analysis, discovered ports/services, compromised hosts, compromised accounts, files transferred, account creation, system modification, AD security analysis, relevant scan data, and any other info necessary to explain specific findings.
At this point we will create a draft report which is our first deliverable to the client. This lets them comment and ask for clarification etc as needed.
### Report Review Meeting
This is where we walk the client through the report. This is typically just an overview and we won't read the entire report word for word, rath we will walk through each finding briefly and give an explanation. 
### Deliverable Acceptance
Scope of Work should clearly define the acceptance of any project deliverables. Generally you submit the draft marked as a draft then the final report marked as the FINAL report. 
### Post-remediation Testing
Most engagements will include post-remediation testing as port of the total cost. We will review any documentation from the client showing remediation and re-test the finding. For each finding, we will want to show evidence that the issue is or is no longer present. 
### Role of the Pentester in Remediation
It may be hard but it is critical that we do NOT remediate items for the client. We need to remain impartial assessors. Remediating things ourselves can create a conflict of interest.
### Data Retention
Your firm should have data retention policies in place. Ensure that they follow all appropriate laws and guidelines. Generally you will retain data for a finite period of time to help with remediation, post-remediation questions etc. Data should be encrypted at rest and deleted after the proper amount of time.
### Close out
Once we have finished everything above, delivered our final report, conducted our report review and post-remediation we need to wipe or destroy all systems involved in testing. Any Data should be kept or retained properly in alignment with policy and contractual obligations. Lastly we bill the client and likely perform a client satisfaction survey. Remember clients will remember interactions not exploits. At the end of the day you need to be a respectful polite contractor who people WANT to work with. 