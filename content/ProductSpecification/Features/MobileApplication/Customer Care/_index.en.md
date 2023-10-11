---
title: Customer Care
tags : ["Composing"]
---

## Introduction
Customer Care or Help is one of the basic features of the software product. By using this feature, Survey User can call the tech support and clarify his/her doubts.

## Business Assumptions
1. Customer Care feature should be planned at the design phase.
1. Survey User can able to call tech support and get support to continue the survey.

## Requirements

### Functional Requirements
1. Valid phone numbers are required.

### Non-functional Requirements
1. User should allow Phone permission in App.
1. If one phone number is busy, Survey User can able to call other number.

### Problem Statement
Customer Care feature is required to get the support from tech team during the survey.

### Design
1. Customer Care page contains six buttons.
1. Click on the button, allow user to call the phone number.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Side Menu|[Side Menu]({{< ref "Side Menu" >}})|Parent Page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_customer_care_btn|To navigate the user to Customer Care page|
|uc_customer_care_number_btn|To contact the respective tech support|

#### KV Database Keys
|KV Database Key|
|---------------|
|SUPPORT_LINE01|
|SUPPORT_LINE02|
|SUPPORT_LINE03|
|SUPPORT_LINE04|
|SUPPORT_LINE05|
|SUPPORT_LINE06|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set Layout/API|KV Database Key|SQLite Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|---------------------------------|------------|------------------------|------|------|------|----|----|------|-------|
|-|-|-|-|-|-|-|-|-|-|-|-|-|

#### ENUM CONSTANTS
No Enum Constants for this feature.

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
|1. Survey User can able to contact tech support during the survey.|

## User Experience
### Customer Care Page buttons
{{<mermaid align="left">}}
graph LR
    CustomerCareOne[Customer care 1]-->CustomerCareTwo[Customer care 2]-->CustomerCareThree[Customer care 3]-->CustomerCareFour[Customer care 4]-->CustomerCareFive[Customer care 5]-->CustomerCareSix[Customer care 6]   
{{< /mermaid >}}


### State Machine
{{<mermaid align="center">}}
flowchart TD
    Start((start))
	SideMenu[App Side Menu]
	CustomerCaretBtn[Customer Care Button]
	CustomerCareFragment[Customer Care Page]
	PhoneNumberCard[Customer Care 1-6 Numbers]
	showExceptionAlert>Show Exception Message]
	showDialDialog[show Dial Option Dialog]
	End((end))
	Start-->SideMenu
	SideMenu--C-->CustomerCaretBtn
	CustomerCaretBtn--S-->CustomerCareFragment
	CustomerCaretBtn--F-->showExceptionAlert
	CustomerCareFragment--C-->PhoneNumberCard
	PhoneNumberCard--S-->showDialDialog
	PhoneNumberCard--F-->showExceptionAlert
	showDialDialog-->End
	showExceptionAlert-->End
	%%For click Representation
	linkStyle 1 stroke:blue,stroke-width:2px;
	linkStyle 4 stroke:blue,stroke-width:2px;
	%%For success Representation
	linkStyle 2 stroke:green,stroke-width:2px;
	linkStyle 5 stroke:green,stroke-width:2px;
	%%For fail Representation
	linkStyle 3 stroke:red,stroke-width:2px;
	linkStyle 6 stroke:red,stroke-width:2px;	
{{< /mermaid >}}

### Flowchart
{{<mermaid align="center">}}
%%{init: {'themeVariables': {'edgeLabelBackground':'#FFFF', 'tertiaryColor': '#fff0f0'}}}%%
flowchart
    Start((start))
    End((end))
    SideMenu[Side Menu]
    CustomerCarePage[Customer Care Page]
    getPhoneNumbers[get Phone Numbers From KV Database]
    CheckCallPhone{Check CALL_PHONE Permission}
    RequestPermission[Request Permission]
    Dialog[Dial Dialog]
    Start-->SideMenu
    SideMenu--Click Customer Care-->CustomerCarePage
    CustomerCarePage-->getPhoneNumbers
    getPhoneNumbers-->CheckCallPhone
    CheckCallPhone--Accepted-->Dialog
    CheckCallPhone--Not Accepted-->RequestPermission
    RequestPermission-->CheckCallPhone
    Dialog-->End
    
    
    
{{< /mermaid >}}

### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant CustomerCare as Customer Care Fragment
    participant KVDB as KV Database
    autonumber 
    rect rgb(244,244,244)
        CustomerCare->>+KVDB: get Key Values : SUPPORT_LINE01,SUPPORT_LINE02,SUPPORT_LINE03,SUPPORT_LINE04,SUPPORT_LINE05,SUPPORT_LINE06
        KVDB-->>-CustomerCare: Values of : SUPPORT_LINE01,SUPPORT_LINE02,SUPPORT_LINE03,SUPPORT_LINE04,SUPPORT_LINE05,SUPPORT_LINE06
    end          
{{< /mermaid >}}

## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
|-|-|-|

## Security compliance check
1. Only Survey User should get the tech support.

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




 
