---
title: Start / Continue Survey
tags : ["Composing"]
---

## Introduction
Start / Continue Survey feature is the starting step to begin the survey. This feature contains properties buttons. Using the buttons Survey User can navigate to property listing page.

## Business Assumptions
1. Start / Continue Survey feature should be planned at the design phase.
1. User should be in the panchayat level to create the property.

## Requirements
### Functional Requirements
1. To start the survey, Survey User should complete the Panchayat Selection process. 

### Non-functional Requirements


### Problem Statement
Start / Continue Survey feature is required to start the survey and to create the properties.

### Design 
1. Start / Continue page contains properties buttons.
1. After clicking the required property button, navigate the user to the respective property listing page.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Panchayat Selection|[Panchayat Selection]({{< ref "PanchayatSelection" >}})|After the selection of panchayat only, user can view the stat/continue survey page.|


#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_start_or_continue_survey_btn|To navigate the user to the start / continue survey page|
|uc_house_btn|To navigate the user to the House listing page|
|uc_auction_btn|To navigate the user to the Auction listing page|
|uc_advertisement_btn|To navigate the user to the Advertisement listing page|
|uc_trade_license_btn|To navigate the user to the TradeLicense listing page|
|uc_kolagaram_btn|To navigate the user to the Kolagaram listing page|
|uc_locked_property_btn|To navigate the user to the Locked Property listing page|
|uc_vacant_land_btn|To navigate the user to the VacantLand listing page|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set Layout/API|KV Database Key|SQLite Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|---------------------------------|------------|------------------------|------|------|------|----|----|------|-------|
|-|-|-|-|-|-|-|-|-|-|-|-|-|


#### ENUM CONSTANTS

No Enum Constants

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
|1. Survey User can able to view the properties buttons and navigate to a particular property listing page after a button click.|

## User Experience

### Start /Continue Survey Page
{{<mermaid align="left">}}
graph LR
    HouseBtn[House Button]-->AuctionBtn[Auction Button]-->AdvertisementBtn[Advertisement Button]-->TradeLicenseBtn[Trade License Button]-->KolagaramBtn[Kolagaram Button]-->LockedPropertyBtn[Locked Property Button]-->VacantLandBtn[Vacant Land Button]
{{< /mermaid >}}



### State Machine
{{<mermaid align="left">}}
flowchart TD
    Start((Start))
    SideMenu[App Side Menu]
    StartOrContinueSurveyBtn[Start / Continue Survey Button]
	SurveyItemsPage[Survey Dashboard]
	PropertyBtn[Required Property Button]
	SideMenuBtn[App Bar Side Menu Button]
	ListingPage[Property Listing Page]
	ErrorAlert1>Exception Error Alert]
	ErrorAlert2>Exception Error Alert]
	ErrorAlert3>Exception Error Alert]
	End((end))
    Start-->SideMenu
    subgraph Side Menu
        SideMenu--C-->StartOrContinueSurveyBtn
        StartOrContinueSurveyBtn--S-->SurveyItemsPage
        StartOrContinueSurveyBtn--F-->ErrorAlert1
    end
    subgraph Start/Continue Survey Page
        SurveyItemsPage--C-->PropertyBtn
        PropertyBtn--S-->ListingPage
        PropertyBtn--F-->ErrorAlert2
    end
    subgraph SideMenu Btn Click In Start / Survey Continue Page
        SurveyItemsPage--C-->SideMenuBtn
        SideMenuBtn--S-->SideMenu
        SideMenuBtn--F-->ErrorAlert3    
    end
    ListingPage-->End
	%%For click Representation
	linkStyle 1 stroke:blue,stroke-width:2px;
	linkStyle 4 stroke:blue,stroke-width:2px;
	linkStyle 7 stroke:blue,stroke-width:2px;
	%%For success Representation
	linkStyle 2 stroke:green,stroke-width:2px;
	linkStyle 5 stroke:green,stroke-width:2px;
	linkStyle 8 stroke:green,stroke-width:2px;
	%%For failure Representation
	linkStyle 3 stroke:red,stroke-width:2px;
	linkStyle 6 stroke:red,stroke-width:2px;
	linkStyle 9 stroke:red,stroke-width:2px;
{{< /mermaid >}}

|Symbol|Action|
|:-----|:----|
|Property|House, Auction, Advertisement, TradeLicense, Kolagaram, Locked Property, VacantLand|
|C|ClickOn|
|S|OnSuccess|
|F|OnFailure|
|Blue Link|Click|
|Green Link|Success|
|Red Link|Failure|


### Sequence Diagram


## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
|-|-|-|
|-|-|-|

## Security compliance check
1. Only Survey User should Create, View Properties through start / continue Survey feature.

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




 
