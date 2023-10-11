---
title: VacantLand Property
tags : ["Composing"]
---

## Introduction
VacantLand Property is one of the basic features of the software product which contains the data of all the VacantLand properties in the Telangana state. 
Vacant land means property land that has no buildings on it and is not being used. By using this VacantLand property feature, Survey User can store every VacantLand property in the panchayat.

## Business Assumptions
1. VacantLand Property feature should be planned at the design phase.
1. User should be in the panchayat level to create the VacantLand property.
1. Owner Aadhaar details are required to create the VacantLand property.
1. Survey User can able to sync the VacantLand property to GS-Cloud.

## Requirements
### Functional Requirements
1. To create VacantLand Property Survey User should complete the Panchayat Selection process. 
1. Once VacantLand property synced, user not allowed to update it.

### Non-functional Requirements
1. Multiple users can create VacantLand property in the same panchayat.
1. One citizen can have multiple VacantLand properties in the same panchayat or different panchayats.

### Problem Statement
VacantLand Property feature is required to store all the VacantLand property details in the panchayat level.

### Design 
1. Each VacantLand property has an Aadhaar Input Type, photo, owner's Aadhaar number, Name, Surname, Father/Spouse Name, Mobile Number, Gender, Date Of Birth, Age, Street Name, Area, Latitude, Longitude, and Survey Pending Status fields.
1. Survey User can Create, View, Update, remove and search the VacantLand property.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Start / Continue Survey|[Start / Continue Survey]({{< ref "StartOrContinueSurvey" >}})|Parent Page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_vacant_land_property_create|To create the VacantLand property|
|uc_vacant_land_property_view|To view the VacantLand property|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set Layout/API|KV Database Key|SQLite Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|---------------------------------|------------|------------------------|------|------|------|----|----|------|-------|


#### ENUM CONSTANTS

##### Aadhaar Input Type

{{<mermaid align="left">}}
classDiagram
    class AadhaarInputType{
      OCR
      QRCODE
      MANUAL
    }
{{< /mermaid >}}



#### Feature Permission
|Permission code|Action|
|---------------|-------|
|-|-|
|-|-|


#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|id|


## Acceptance Criteria
|Description|
|-------------|
|Version : 1.0|
|1. Survey User can able to Create, View, Update, Search, Delete and Sync the VacantLand Property.|

## User Experience

### State Machine

### Flowchart

### Sequence Diagram


## Unit Test Cases
#### Authorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create |ut_p_c_GSTS_PROPERTY_DATASYNC_API_100 ut_n_c_GSTS_PROPERTY_DATASYNC_API_200 ut_n_c_GSTS_PROPERTY_DATASYNC_API_300 |**Positive Test Cases:** Vacant Land Data Sync Postive Test Cases Combination-01 **Negative Test Cases:** 1.Vacant Land Data Sync Negative Test Cases Combination-02 2.Vacant Land Data Sync Negative Test Cases Combination- Create Vacant Land Property Without DB Connection|**id**: 1.Valid Id **address:** 1.Valid Characters 2.length>6 and length<128 3.null **area:**  1.null 2.Value > 0 **latitude** **longitude** **aid:** 1.Valid characters 2.length=12 3.null **name:** 1.Valid Characters 2.length>3 and length<64 3.null **surname:** 1.Valid Characters 2.length>1 and length<32 3.null **fsname:** 1.Valid Characters 2.length>3 and length<64 3.null **gender** **age** **dob** **mobile:** 1.Valid Characters [starts with 6,7,8,9] 2.length=10 3.null **aadhaarInputType** **surveyEndTime** **surveyStartTime**|5|5|10|vacantLandPropertyDataSyncPosTC01, vacantLandPropertyDataSyncNegTC02, vacantLandPropertyDataSyncNegTC03|
|1.0| View |ut_n_v_GSTS_PROPERTY_DATASYNC_API_400|**Negative Test Cases:** Vacant Land Data Sync Negative Test Cases Combination- View Vacant Land Without DB Connection|1.Valid Id|0|1|1|vacantLandPropertyDataSyncNegTC04|

## Security compliance check
1. Only Survey User should Create, View, Update, Delete, Search and Sync the VacantLand Property.

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




 
