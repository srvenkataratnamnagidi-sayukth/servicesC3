---
title: Product Feature Template
tags : ["Composing"]
weight: 5
---
## Instructions to use this Template
1. Copy this page and rename the title to **Name of the JIRA Epic**
1. Remove the section "Instructions to use this Template"
1. Update the associated JIRA Epic description with a link to this page
1. Inline comments should be annotated with the commentator's identify; Once the comment is addressed, inline comments should be removed.

This Technical Spec document should be used to communicate important design information (including, sometimes, the associated requirements). One theme you may notice in the instructions below is the importance of conciseness. We are aiming for enough detail to convey the most important ideas about the design to the following audiences:
1. **Primary**
	+ The implementer (i.e. the developer)
	+ The reviewer(s)
	+ Technical leaders
	+ Those responsible for enhancing or fixing the system in the future
	+ Other development teams responsible for interacting with the system (e.g. consumer teams) QA
1. **Secondary**
	+ Non-technical leaders
	+ Technical writers
	
It is important to put yourself into the mindset of these roles, especially the primary ones, when documenting design to understand what kinds of information needs to be conveyed. There is a critical level of detail that is just right. Going beyond this balanced level risks creating a document which nobody will read or get value from. Consider the use of standards based (i.e. UML) diagrams to supplant long textual descriptions or pseudo code to help achieve this goal.

## Introduction
The introduction should provide a brief overview of the functionality addressed by this specification.
The goal is to provide an initial context to the reader. Details about the requirement or design should be deferred to later sections in the document.
Provide current state of the problem. If required please explain a bit domain knowledge, Notations or acronyms.   

## Business Assumptions
The Business Assumptions aren't requirements, but drive the requirements based on the assumptions we are making about the business. 
These assumptions are to be validated at the end of the release as a learning mechanism to make adjustments to future iterations based on what we learned from validating the assumptions.

## Requirements
This section should elaborate, as necessary, both functional requirements and non-functional requirements and assumptions.
This section is not meant to be a full software requirements specification (SRS) nor actual design. Rather it is an opportunity for the product manager to document the customer needs which the design is intended to solve for. 
This intent is to assist the reader in understanding the problem better. The documentation process itself is helpful in ensuring the design is addressing the correct problems.

### Functional Use cases
Describe requirements in the form of a user story, assumptions, and acceptance criteria:

### Non-functional Use cases
Document any non-functional aspects which are specific to this design such as performance expectations like page load time, number of concurrent users, etc. 
If there are none which are specific to this design (i.e. the requirements are the same as those for the system), then this section can simply state: "Nothing specific to this design noted."

### Problem Statement
Explain the issue in one sentence

### Proposed Solutions
Explain all the Proposed solutions

#### Proposed Solution 01
Explain the Proposed Solution 01 in in brief. Provide detailed Explanation for the Recommended one. 

#### Proposed Solution 02
Explain the Proposed Solution 02 in in brief. Provide detailed Explanation for the Recommended one. 

#### Proposed Solution 03
Explain the Proposed Solution 03 in in brief. Provide detailed Explanation for the Recommended one. 

## User Experience
Link to any UX artifacts (e.g. wireframes, mockups) here. Additional UX related information can be provided, as needed.

## Security compliance check
Each module SHOULD follow the security compliance defined by the security team Security Testing Methodology Some of the important guidelines
1. Don't show/print the Passwords in the Plain Text format in any of the LOGGER, Reports and on Persistence files etc. 
1. Please submit the security scanner report for this feature. Get help from Security team to provide the security report 
1. Do not use the 3rd party modules if they are vulnerable to security compliance

## Operational Enablement
This section will describe the changes to the current production, staging environments

## Deprecation functionality
If this feature can deprecate any of the existing functionalities/features then mention the following
1. How to migrate to new feature?
1. How migrate the current data set?
1. Deprecation date
1. Any other specific notes

## User Manual
Provide all the details to User Manual

## Open JIRA issues list
Please provide the open JIRA issues list here.

|Feature/Defect ID|Link|
|----|----|
|JIRA 01|Link01|


## References
1. Domain knowledge links
1. Other links to consider

|Name|Link|
|----|----|
|Name 01|Link01|

## Development Estimations
1. Provide the Estimations and Due dates
1. Provide Scrum team details

|Release Tag|Feature/Defect ID|Scrum Deatils|Start date|End date|
|-----------|-----------------|-------------|----------|--------|
|tag1|JIRA-001|Scrum W23|MM DD YYYY|MM DD YYYY|

## Feature Doneness Criteria
Check list for the Doneness criteria

|Metric|Unit Measure|Expected Result|Actual Result|Accepted?|Remarks|References|
|------|------------|---------------|-------------|---------|-------|----------|
|Acceptance Criteria Define?|YES or NO||||||
|Architecture Approved?|YES or NO||||||
|Coding Completed?|YES or NO||||||
|Product Defects|Number||||||
|Unit Test Case Count?|Number||||||
|Integration Test Cases Count|Number||||||
|Sonar Vulnerabilities Count|Number||||||
|Code Coverage|Number||||||
|User Manual Verified?|YES or NO||||||
|PenTest Defect Count?|Number||||||
|PM Accepted?|YES or NO||||||
|OM Accepted?|YES or NO||||||
|Deployed to Staging?|YES or NO||||||
|Deployed to Production?|YES or NO||||||




 
