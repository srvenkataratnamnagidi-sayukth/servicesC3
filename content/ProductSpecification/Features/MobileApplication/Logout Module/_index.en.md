---
title: Logout Module
tags : ["Composing"]
---

## Introduction
Log out means to end access to  Application.After Login into the application user can Start the survey.User can create House,Auction,Advertisement,TradeLicense,Kolagaram or VacantLand.After finishing the survey of given properties Survey User will sync the data and complete the survey all these functions are completed then user go for log out.But if survey user click on logout before all these action he/she can re login in to the system   

## Business Assumptions
1. Logout Property feature should be planned at the design phase.
1. User should be in the panchayat level to perform Log out action.

## Requirements
### Functional Requirements
1. User should Log in to the system to log out.

### Non-functional Requirements
1.If multiple users are log-in with same credentials , log out from the device will not affected the log in in ohter devices.

### Problem Statement
Log out helps protect the current user's access or prevent unauthorized actions on the current login session and is thus an important part of the application.

### Design 

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|-|-|-|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_logout_property_logout|To logout from the application|



#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set Layout/API|KV Database Key|SQLite Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|---------------------------------|------------|------------------------|------|------|------|----|----|------|-------|
|NA|NA|NA|NA|NA|NA|NA|NA|NA|NO|NO|NO||

#### Feature Permission
|Permission code|Action|
|---------------|-------|
|-|-|
|-|-|


#### Constraints
|Constraint|Key|
|----------|----|
|-|-|


## Acceptance Criteria
|Description|
|-------------|
|Version : 1.0|
|-|

## User Experience

{{<mermaid align="left">}}
graph LR
    LogoutButton[Logout]   
{{< /mermaid >}}

### State Machine
{{<mermaid align="center">}}
flowchart TD
    SideMenuPage(( Side Menu Page))
	LogoutBtn[Logout Button]
	LoginPage[Login Page]
	SideMenuPage--C-->LogoutBtn
	linkStyle 0 stroke:blue,stroke-width:2px,color:black;
	LogoutBtn--S-->LoginPage
	linkStyle 1 stroke:green,stroke-width:2px,color:black;
	LoginPage--F-->SideMenuPage 
	linkStyle 2 stroke:red,stroke-width:2px,color:black;
{{< /mermaid >}}

| Symbol| Description|
|--|--|
| C| OnClick|
| S| OnSuccess|
| F| OnFailure|

### Flowchart
{{<mermaid align="center">}}
flowchart TD
   Start((start))
{{< /mermaid >}}

## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
|-|-|-|
|-|-|-|

## Security compliance check
1. Nothing specific use case found

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the USER ROles in the User Manual. It's scope is limited to Developer Technical Documentation

## Feature/Defect list
|Feature/Defect ID|Link|Status|
|----|----|---|
|GS-0003|[GS-0003](https://shadkona.atlassian.net/browse/GS-0003)|Closed|


## References

## Development Estimations
|Release Tag|Feature/Defect ID|Scrum Deatils|Start date|End date|
|-----------|-----------------|-------------|----------|--------|
|2020OCT|GS-0002|Scrum 2020OCTs2|14 OCT 2020|28 OCT 2020|

## Feature Doneness Criteria
Check list for the Doneness criteria

|Metric|Unit Measure|Expected Result|Actual Result|Accepted?|Remarks|Approver|
|------|------------|---------------|-------------|---------|-------|----------|
|Acceptance Criteria Defined?|YES or NO|YES|YES|Accepted|All test cases passed|PM|
|Architecture Approved?|YES or NO|YES|YES|Accepted|Design is accepted|Architect|
|Coding Completed?|YES or NO|YES|YES|Completed|Completed|EM|
|Product Defects|Number|0|0|Accepted||EM|
|Unit Test Case Count?|Number|>5|8|Accepted|Tested|EM|
|Integration Test Cases Count|Number|>5|9|Accepted|Tested|EM|
|Sonar Vulnerabilities Count|Number|0|0|Accepted|validated|EM|
|Code Coverage|Number|>98%|99%|Accepted|Validated|EM|
|User Manual Verified?|YES or NO|YES|YES|Accepted|Validated|DocM|
|PenTest Defect Count?|Number|<2|0|Accepted|Validated|EM|
|PM Accepted?|YES or NO|YES|YES|Accepted|Good to go|PM|
|OM Accepted?|YES or NO|YES|YES|Accepted|Good to go|OM|
|Deployed to Staging?|YES or NO|YES|YES|Accepted|Good to go|EM|
|Deployed to Production?|YES or NO|YES|YES|Accepted|Good to go|OM|




 
