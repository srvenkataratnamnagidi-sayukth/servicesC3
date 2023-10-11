---
title: About Page
tags : ["Composing"]
---

## Introduction
About feature is one of the basic features of the software product. It contains details of the project. About feature provides the vision and motto of application to the user.

## Business Assumptions
1. About feature should be planned at the design phase.
1. Survey User can able to view the About page.

## Requirements
### Functional Requirements
1. We have to show project details in about page. Also show app last update time and app version in about page.

### Non-functional Requirements


### Problem Statement
About feature is required to understand the ePanchayat Telangana Survey project details and its motto.

### Design 
1. About page contains ePanchayat Telangana Survey details.
1. About page also contains two labels,named as app update time, app version and their values.


#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Side Menu|[Side Menu]({{< ref "Side Menu" >}})|Parent Page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_about_btn|To view the about page|



#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set Layout/API|KV Database Key|SQLite Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|---------------------------------|------------|------------------------|------|------|------|----|----|------|-------|
|-|-|-|-|-|-|-|-|-|-|-|-|-|

#### Feature Permission
|Permission code|Action|
|---------------|-------|
|-|-|

#### Constraints
|Constraint|Key|
|----------|----|
|-|-|

## Acceptance Criteria
|Description|
|-------------|
|Version : 1.0|
|1. Survey User can able to read the ePanchayat Telangana Survey details.|

## User Experience


### State Machine
{{<mermaid align="center">}}
flowchart TD
    Start((start))
	SideMenu[App Side Menu]
	AboutBtn[About Button]
	AboutFragment[About Page]
	showExceptionAlert>Show Exception Message]
	End((end))
	Start-->SideMenu
	SideMenu--C-->AboutBtn
	AboutBtn--S-->AboutFragment
	AboutBtn--F-->showExceptionAlert
	showExceptionAlert-->End
	AboutFragment-->End
	linkStyle 1 stroke:blue,stroke-width:2px;
	linkStyle 2 stroke:green,stroke-width:2px;
	linkStyle 3 stroke:red,stroke-width:2px;
{{< /mermaid >}}

|Symbol|Action|
|:-----|:----|
|C|ClickOn|
|S|OnSuccess|
|F|OnFailure|
|Blue Link|Click|
|Green Link|Success|
|Red Link|Failure|



### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant About as About Fragment
    participant KVDB as KV Database
    autonumber 
       
    rect rgb(244,244,244)
        About->>+KVDB: get App Update Time & App Version
        KVDB-->>-About: App Update Time , App Version Kv Data
    end
    
{{< /mermaid >}}

## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
|-|-|-|
|-|-|-|

## Security compliance check
1. Only Survey User can view the About page.

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




 
