---
title: Kolagaram Property
tags : ["Composing"]
---

## Introduction
Kolagaram Property is one of the features of the software product which contains the data of all the Kolagarams properties in the Telangana state.  A Kolagaram is a village level small industry.
By using this Kolagaram property feature, Survey User can store every Trade License property in the panchayat.

## Business Assumptions
1. Kolagaram Property feature should be planned at the design phase.
1. User should be in the panchayat level to create the kolagaram property.
1. Owner Aadhaar details are required to create the kolagaram property.
1. Survey User can able to sync the kolagaram property to GS-Cloud.

## Requirements
### Functional Requirements
1. To create kolagaram Property Survey User should complete Panchayat Selection process. 
1. Only one kolagaram property is allowed with the same name.
1. Only one kolagaram property is allowed with the same GPSanctionId.
1. After Kolagaram property synced, user not allowed to update it.

### Non-functional Requirements
1. Multiple users can create kolagaram property in the same panchayat.
1. Multiple users can create same kolagaram property in the same panchayat. But only one Kolagaram Property will sync among all users based on who sync first.
1. One citizen can have multiple kolagaram properties in the same panchayat or different panchayats.

### Problem Statement
Kolagaram Property feature is required to store all the kolagaram property details in the panchayat level.

### Design 
1. Each Kolagaram property has an Aadhaar Input Type, owner's Aadhaar number, Name,Surname, Father/Spouse Name,Mobile Number,Gender,Date Of Birth,Age,Kolagaram Name,Street Name, GP Sanction Id, Goods Type, Annual Turnover,Motor Capacity, Latitude, Longitude, and Survey Pending Status fields.
1. Survey User can Create, View, Update, remove and search the kolagaram property.
1. Only one kolagaram property is allowed with the same name.
1. Only one kolagaram property is allowed with the same GPSanctionId.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Start / Continue Survey|[Start / Continue Survey]({{< ref "StartOrContinueSurvey" >}})|Parent Page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_kolagaram_property_create|To create the kolagaram property|
|uc_kolagaram_property_view|To view the kolagaram property|


#### Model Attributes

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

##### Kolagaram Category

{{<mermaid align="left">}}
classDiagram
    class KolagaramCategory{
      NONE
      BRICKS
      CEMENT_BRICKS
      EGGS
      COMMERCIAL_CROPS
      GLASS_BEADS
      OTHER
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
|Unique Keys|1. kolagaram_name|
||2. gp_sanction_id|

## Acceptance Criteria
|Description|
|-------------|
|Version : 1.0|
|1. Survey User can able to Create, View, Update, Search, Delete and Sync the Kolagaram Property.|

## User Experience

### State Machine

### Flowchart

### Sequence Diagram

## Unit Test Cases
#### Authorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create |ut_p_c_GSTS_KOLAGARAM_PROPERTY_DATASYNC_API_100 ut_n_c_GSTS_KOLAGARAM_PROPERTY_DATASYNC_API_200 ut_n_c_GSTS_KOLAGARAM_PROPERTY_DATASYNC_API_300 |**Positive Test Cases:** 1.Kolagaram Data Sync Postive Test Cases Combination-01  **Negative Test Cases:** 1.Kolagaram Data Sync Negative Test Cases Combination-02 2.Negative Case - Sync Kolagaram Property without DB Connection |   **id**: 1.Valid Id **address:** 1.Valid Characters 2.length>6 and length<128 3.null **kolagaramName**: 1.Valid Characters 2.length>3 and length<64 3.null **goodsType** **horsePower:** **gpSanctionId** **goodsValue** **latitude** **longitude** **aid:** 1.Valid characters 2.length=12 3.null **name:** 1.Valid Characters 2.length>3 and length<64 3.null **surname:** 1.Valid Characters 2.length>1 and length<32 3.null **fsname:** 1.Valid Characters 2.length>3 and length<64 3.null **gender** **age** **dob** **mobile:** 1.Valid Characters [starts with 6,7,8,9] 2.length=10 3.null **aadhaarInputType** **surveyEndTime** **surveyStartTime**|7|8|15|kolagaramPropertyDataSyncPosTC01, kolagaramPropertyDataSyncNegTC02, syncKolagaramPropertyWithoutDbConnectionNeg|
|1.0| View |ut_n_c_GSTS_KOLAGARAM_PROPERTY_DATASYNC_API_400|**Negative Test Cases:** 1.Negative Case - View Kolagaram Property without DB Connection|1.Valid Id|0|1|1|viewKolagaramPropertyWithoutDbConnectionNeg|

## Security compliance check
1. Only Survey User should Create, View, Update, Delete, Search and Sync the Kolagaram Property.

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




 
