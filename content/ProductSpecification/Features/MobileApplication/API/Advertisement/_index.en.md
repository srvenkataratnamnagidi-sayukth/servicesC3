---
title: Advertisement Property
tags : ["Composing"]
---

## Introduction
Advertisement Property is one of the basic features of the software product which contains the data of all the 
advertisement properties in the Telangana state.Places belonging to the government are given for citizens to advertise their product in this adveritsement module.By using this advertisement property feature we have to store 
every advertisement property data and know about every advertisement property in the state. Every advertisement 
property should be stored under the respective panchayat only.

## Business Assumptions
1. Advertisement Property feature should be planned at the design phase.
1. User should be in the panchayat level to create the advertisement property.
1. Owner Aadhaar number is required to create the advertisement property.
1. Survey User can able to sync the Advertisement Property to GS-Cloud.

## Requirements
### Functional Requirements
1. Advertisement Property feature only accessible at the panchayat level.
1. GP-Saction id is unique in the advertisement property
1. After Advertisement property synced, user not allowed to update it.

### Non-functional Requirements
1. Multiple users can create Advertisement property in the same panchayat.
1. Multiple users can create same Advertisement property in the same panchayat.But only one Advertisement Property will sync among all users based on who sync first.
1. One citizen can have multiple Advertisement properties in the same panchayat or different panchayats.

### Problem Statement
Advertisement Property feature is required to store all the Advertisement property details in the panchayat level.

### Design 
1. Each Advertisement property has Advertisement Name, Street Name, GP Sanction Id, Advertisement Category,Advertisement Asset, Number Of Installments fields.
1. Survey User can Create, View, Update, Delete and search in the Advertisement Property.
1. Only one Advertisement Property is allowed with the same name.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Start / Continue Survey|[Start / Continue Survey]({{< ref "StartOrContinueSurvey" >}})|Parent Page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_advertisement_property_create|To create the Advertisement Property|
|uc_advertisement_property_view|To view the Advertisement Property|


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

##### Advertisement Category
{{<mermaid align="left">}}
classDiagram
    class AdvertisementCategory{
      NONE
      GROUND_BASED
      MOVING
      LIGHTING
    }
{{< /mermaid >}}
#### Advertisement Asset
{{<mermaid align="left">}}
classDiagram
    class AdvertisementAsset{
      NONE
      PUBLIC
      PRIVATE
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
|Unique Keys|1. gp_sanction_id 2. advertisement_name|

## Acceptance Criteria
|Description|
|-------------|
|Version : 1.0|
|1. Survey User can able to Create, View and Sync the Advertisement Property.|

## User Experience

### State Machine

### Flowchart

### Sequence Diagram

## Unit Test Cases
#### Authorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create |ut_p_c_GSTS_ADVERTISEMENT_PROPERTY_DATASYNC_API_100 ut_n_c_GSTS_ADVERTISEMENT_PROPERTY_DATASYNC_API_200 ut_n_c_GSTS_ADVERTISEMENT_PROPERTY_DATASYNC_API_300 |**Positive Test Cases:** 1.Advertisement Data Sync Postive Test Cases Combination-01  **Negative Test Cases:** 1.Advertisement Data Sync Negative Test Cases Combination-02 2.Negative Case - Sync Advertisement Property without DB Connection |   **id**: 1.Valid Id **address:** 1.Valid Characters 2.length>6 and length<128 3.null **advertisementName**: 1.Valid Characters 2.length>3 and length<64 3.null **assetType** **baseValue:** **block** **boardLocation** **boardSize** **category** **numberOfInstallments** **gpSanctionId** **latitude** **longitude**  **taxEndDate** **taxStartdate** **aid:** 1.Valid characters 2.length=12 3.null **name:** 1.Valid Characters 2.length>3 and length<64 3.null **surname:** 1.Valid Characters 2.length>1 and length<32 3.null **fsname:** 1.Valid Characters 2.length>3 and length<64 3.null **gender** **age** **dob** **mobile:** 1.Valid Characters [starts with 6,7,8,9] 2.length=10 3.null **aadhaarInputType** **surveyEndTime** **surveyStartTime**|5|9|14|advertisementPropertyDataSyncPosTC01, advertisementPropertyDataSyncNegTC02, syncAdvertisementPropertyWithoutDbConnectionNeg, viewAdvertisementPropertyWithoutDbConnectionNeg|
|1.0| View |ut_n_c_GSTS_ADVERTISEMENT_PROPERTY_DATASYNC_API_400|**Negative Test Cases:** 1.Negative Case - View Advertisement Property without DB Connection|1.Valid Id|0|1|1|viewAdvertisementPropertyWithoutDbConnectionNeg|

## Security compliance check
1. Only Survey User should Create, View, Update, Delete, Search and Sync the Advertisement Property.

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




 
