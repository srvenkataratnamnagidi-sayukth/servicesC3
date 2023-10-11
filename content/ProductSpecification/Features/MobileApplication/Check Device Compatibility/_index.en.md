---
title: Check Device Compatibility
tags : ["Composing"]
---

## Introduction
Check Device Compatibility feature is one of the basic features of the software product. By Using this feature, 
Surveyor have to know that whether the mobile device is compatible to take the Survey or Not.The asset survey application needs
some features in surveyor mobile device to take the survey,So that purpose we design the Check Device Compatibility feature.This feature will check and certify whether
mobile phone can be used for this survey or not.
## Business Assumptions
1. Check Device Compatibility feature should be planned at the design phase.
1. Any one who have this Application can view the ***Check Device Compatibility*** feature.

## Requirements
### Functional Requirements
1. In this feature we have to check the below features to decide the whether the device is compatible to take the Survey.
    1. Android os version. 
    1. Wi-fi Connectivity.
    1. Mobile data Connectivity.
    1. Gps Availability
    1. Camera Support
    1. Location Coordinates
1. Android os version must be greater than 5.0.0.
1. Wi-fi Connectivity must be Available
1. Mobile data connectivity must be Available.
1. Gps must be Available
1. Camera must be supported.
1. If the mobile phone has all the features,then it will display your mobile phone is compatible else it will display
   your Mobile phone is not compatible.

    

    

### Non-functional Requirements
1.Any User Can check the Compatibility of the mobile device.


### Problem Statement
Check Device Compatibility feature is required to know whether the device is compatible to take the Survey.

### Design 

1. In this feature we have **two** pages
   1. Device Compatibility Check Page.
   1. Device Status Page.
#### Device Compatibility Check Page
This page Contains "Start Compatibility Check" button which is used to navigate to the "Device Status" Page.
#### Device Status Page.
This page contains the Android Os Version,Wi-fi Connectivity,Mobile Data Connectivity,GpsAvailable,Camera Support and Location Coordinates which are ***CardViews***.
These are used to display the status of respective CardViews.
#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|


#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_Start_Compatibility_Check_btn|To Check the  device status, and navigate the  "Compatibility Check page to "Device Status Page" |



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
|1. Any User who have the application can able view and check the device status.|

## User Experience

#### Device Compatibility Check Page
{{<mermaid align="center">}}
  graph LR
   startCompatibilityCheckBtn[Start Compatibility Check Button]
   BackBtn[<- Back Button]
   startCompatibilityCheckBtn-->BackBtn
   
{{< /mermaid >}}

#### Device Status Page
  {{<mermaid align="center">}}
    graph LR
     DoneBtn[Done Button]
     BackBtn[<- Back Button]
     DoneBtn-->BackBtn
     
  {{< /mermaid >}}



### State Machine
{{<mermaid align="center">}}
flowchart TD
    Start((start))
	HomePage[Home Page]
	CheckDeviceCompatibilityBtn[Check Device Compatibility Button]
	subgraph Device Compatibility Check Page
	    DeviceCompatibilityCheckPage[Device Compatibility Check Page]
	    startCompatibilityCheckBtn[Start Compatibility Check Button]
	    BackBtn[Back Button]
	 end   
	subgraph Device Status Page
	    DeviceStatusPage[Device Status Page]
	    DoneBtn[Done Button]
	    BackBtn1[Back Button]
	end  
	%%Home Page 
	Start-->HomePage
	HomePage--C-->CheckDeviceCompatibilityBtn
	linkStyle 1 stroke:blue,stroke-width:2px;
	CheckDeviceCompatibilityBtn--S-->DeviceCompatibilityCheckPage
	linkStyle 2 stroke:green,stroke-width:2px;
	CheckDeviceCompatibilityBtn--F-->HomePage
	linkStyle 3 stroke:red,stroke-width:2px;
	
	%%Device Compatibility Check Page
	DeviceCompatibilityCheckPage--C-->startCompatibilityCheckBtn
	linkStyle 4 stroke:blue,stroke-width:2px;
	startCompatibilityCheckBtn--S-->DeviceStatusPage
    linkStyle 5 stroke:green,stroke-width:2px;
    startCompatibilityCheckBtn--F-->DeviceCompatibilityCheckPage
    linkStyle 6 stroke:red,stroke-width:2px;
    
    %%BackButton
    DeviceCompatibilityCheckPage--C-->BackBtn
    linkStyle 7 stroke:blue,stroke-width:2px;
    BackBtn--S-->HomePage
    linkStyle 8 stroke:green,stroke-width:2px;
    BackBtn--F-->DeviceCompatibilityCheckPage
    linkStyle 9 stroke:red,stroke-width:2px;
        
    %%Device Status Page
    DeviceStatusPage--C-->DoneBtn
    linkStyle 10 stroke:blue,stroke-width:2px;
    DoneBtn--S-->HomePage
    linkStyle 11 stroke:green,stroke-width:2px;
    DoneBtn--F-->DeviceStatusPage
    linkStyle 12 stroke:red,stroke-width:2px;
    DeviceStatusPage--C-->BackBtn1
    linkStyle 13 stroke:blue,stroke-width:2px;
    BackBtn1--S-->DeviceCompatibilityCheckPage
    linkStyle 14 stroke:green,stroke-width:2px;
    BackBtn1--F-->DeviceStatusPage
    linkStyle 15 stroke:red,stroke-width:2px;
	
	
{{< /mermaid >}}

|Symbol|Action|
|:-----|:----|
|C|ClickOn|
|S|OnSuccess|
|F|OnFailure|
|Blue Link|Click|
|Green Link|Success|
|Red Link|Failure|


## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
|-|-|-|
|-|-|-|

## Security compliance check
1. Any User can view the Check Device Compatibility page.

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




 
