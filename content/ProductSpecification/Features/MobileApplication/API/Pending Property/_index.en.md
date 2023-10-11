---
title: Locked Property
tags : ["Composing"]
---

## Introduction
Locked Property is one of the basic features of the software product which contains the data of all the Locked properties in the Telangana state. By using this Locked property feature we have to store every Locked property data and know about every Locked property in the state. Every Locked property should be stored under the respective panchayat only. Locked property means the property belongs to the government or no owner is there for property.

## Business Assumptions
1. Locked Property feature should be planned at the design phase.
1. User should be in the panchayat level to create the Locked property.
1. Survey User can able to sync the Locked property to GS-Cloud.

## Requirements
### Functional Requirements
1. Locked Property feature only accessible at the panchayat level.
1. Only one Locked property is allowed with the same name for similar property.
1. If Locked Property is House then with same door number two properties are not allowed.
1. After Locked property synced, user not allowed to update it.

### Non-functional Requirements
1. Multiple users can create Locked property in the same panchayat.
1. Multiple users can create same Locked property in the same panchayat.But only one Locked Property will sync among all users based on who sync first.


### Problem Statement
Locked Property feature is required to store all the Locked property details in the panchayat level.

### Design 
1. In Each Locked property (ifPropertyName is House) then we have  Property Type,Door Number, Street, Latitude, Longitude, Building Category,Building Sub Category,Length,Breadth,Site Area,Land Survey Number, Land Record Type,Legal Issue,Building Number,Roof Type, Building Floor Type, Construction Status,Construction Completed Date, Plingth Length,Plingth Breadth,Plingth Area,and Survey Pending Status fields.
1. In Each Locked property (ifPropertyName is !=House) then we have Property Type, Name, Street ,Latitude,Longitude and Survey Pending
1. Only one locked property is allowed with the same name or Door Number.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Start / Continue Survey|[Start / Continue Survey]({{< ref "StartOrContinueSurvey" >}})|Parent Page|


#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_locked_property_create|To create the Locked property|
|uc_locked_property_view|To view the Locked property|


#### Model Attributes

#### ENUM CONSTANTS

##### Aadhaar Input Type

{{<mermaid align="left">}}
classDiagram
    class PropertyType{
      HOUSE
      AUCTION
      ADVERTISEMENT
      TRADE_LICENSE
      KOLAGARAM
      VACANT_LAND
      OTHER
    }
{{< /mermaid >}}
#### Building Category
{{<mermaid align="left">}}
classDiagram
    class BuildingCategory{
      NONE
      RESIDENTIAL
      ADVERTISEMENT
      COMMERCIAL
      EXEMPTION
    }
{{< /mermaid >}}

##### Roof Type

{{<mermaid align="left">}}
classDiagram
    class RoofType{
      RCC
      AC_SHEETS_OR_ZINK_SHEETS
      COUNTRY_OR_MANGALORE_TILES
      SHABAD_STONES
      TATCHED_OR_MUD_ROOF
      NONE
    }
{{< /mermaid >}}

##### Building Sub Category

{{<mermaid align="left">}}
classDiagram
    class BuildingSubCategory{
      None
      ARV or CAP Exemption
      CHOULTARIES
      EDUCATIONAL_INSTITUTIONS 
      ANCIENT_MONUMENTS
      CHARITABLE_HOSPITAL
      OTHER
      GRAM_PANCHAYAT_PROPERTY
      TEMPLES
      CENTRAL_OR_STATE_PROPERTY
      CHURCH
      MAZEED
      WAQF_BOARD_PROPERTY
      ELECTRICITY_TRANSCO
      RTC
      COLLAPSED_HOUSE
      OPEN_LANDS
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
|Unique Keys|name|

## Acceptance Criteria
|Description|
|-------------|
|Version : 1.0|
|1. Survey User can able to Create, View, Sync the Locked Property.|

## User Experience


### State Machine


## Unit Test Cases
#### Authorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create |ut_p_c_GSTS_PENDING__PROPERTY_DATASYNC_API_100 ut_n_c_GSTS_PENDING_PROPERTY_DATASYNC_API_200 ut_n_c_GSTS_PENDING_PROPERTY_DATASYNC_API_250 ut_n_c_GSTS_PENDING_PROPERTY_DATASYNC_API_270 ut_n_c_GSTS_PENDING_PROPERTY_DATASYNC_API_300 |**Positive Test Cases:** PendingProperty Data Sync Postive Test Cases Combination-01 **Negative Test Cases:** 1.PendingProperty Data Sync Negative Test Cases Combination-02   2.Negative Case - Create Pending House Property - Floor 0 roof type is SHADAB STONES and Floor 1 roof type is RCC   3.Negative Case - Create Pending House Property - Floor 1 plinth length and plinth breadth is greater than Floor 0   4.Negative Case - Sync Pending Property without DB Connection||5|7|12|pendingPropertyDataSyncPosTC01, pendingPropertyDataSyncNegTC02,  pendingHousePropertyDataSyncNegTC03 pendingHousePropertyDataSyncNegTC04,  syncPendingPropertyWithoutDbConnectionNeg|
|1.0| View |ut_n_v_GSTS_PENDING_PROPERTY_DATASYNC_API_400|**Negative Test Cases:** Negative Case - View Pending Property without DB Connection|1.Valid Id|0|1|1|viewPendingPropertyWithoutDbConnectionNeg|


## Security compliance check
1. Only Survey User should Create, View, Sync the Locked Property.

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual

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




 
