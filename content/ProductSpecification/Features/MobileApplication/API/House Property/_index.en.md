---
title: House Property API
tags : ["Composing"]
---

## Introduction
House Property is one of the basic features of the software product which contains the details of all the house properties in the Telangana state. By using this house property feature we have to store every house data and know about every house property in the state.House property should be stored under the respective panchayat only. House Module feature embedded in the house property. While creating house property, house module details are also collected and stored.

## Business Assumptions
1. House Property feature should be planned at the design phase.
1. User should be in the panchayat level to create the house property.
1. Door Number is required to create the house property.

## Requirements
### Functional Requirements
1. House Property feature only accessible at the panchayat level.
1. While creating house property, the Door Number will bind to it.
1. Only one house property is allowed with the same Door Number.

### Non-functional Requirements
1. Multiple users can create house property in the same panchayat.
1. One citizen can have multiple houses in the same panchayat or different panchayats.

### Problem Statement
House Property feature is required to store all the house property details in the panchayat level.

### Design 
1. In each House property If OwnHouse is Yes then house module will have Door Number,Street Name, Block/Ward Number,Building Category,Length,Breadth, Site Area,Land Survey Number,Land Record Type and Legal Issue.
1. In each House property If OwnHouse is No then house property will have Aadhhar Input Type,Aadhaar Number,Name,Surname,Father/SpouseName,Mobile Number,Gender,Date Of Birth,Age and Marital Status these are Additional information we take from households. 
1. Each House Module has Building Number, Building Floor Number, Roof Type, Construction Type, Plinth Length, Plinth Breadth, Plinth Area, and Tax Start Date.
1. Each House module have amenities like Private Water Taps,Electricity Connections,LPG Connections,Toilet Count,Soak Pits,Trees Count,Drainage Type, Road Type,Latitude and Longitude.
1. We can Create, View the house property.
1. Only one house property is allowed with the same Door Number.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Start/Continue Survey|[Start/Continue Survey]({{< ref "side menu" >}})|Parent Page|


#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_house_property_create|To create the house property|
|uc_house_property_view|To view the house property|


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

##### House Category

{{<mermaid align="left">}}
classDiagram
    class HouseCategory{
      RESIDENTIAL
      COMMERCIAL
      EXEMPTION
      NONE
    }
{{< /mermaid >}}

##### Commercial Type

{{<mermaid align="left">}}
classDiagram
    class CommercialType{
      SHOPS
      OFFICES_AND_BANKS
      HOSPITAL_AND_NURSING_HOME
      EDUCATIONAL_INSTITUTIONS
      HOTELS_LODGING_AND_RESTAURANTS
      GODOWNS
      INDUSTRIES
      CINEMA_THEATRES
      OTHERS
	  NONE
    }
{{< /mermaid >}}

##### Exemption Type

{{<mermaid align="left">}}
classDiagram
    class ExemptionType{
      ARV_OR_CAP_EXEMPTION
      CHOULTARIES
      EDUCATIONAL_INSTITUTIONS
      ANCIENT_MONUMENTS
      CHARITABLE_HOSPITALS
      PUBLIC_WORSHIP
      OTHERS
      GP_PROPERTY
      TEMPLES
      CENTRAL_OR_STATE_PROPERTY													
	  CHURCH
	  MAZEED
	  WAQF_BOARD_PROPERTY
	  ELECTRICITY_TRANSCO
	  RTC
	  COLLAPSED_HOUSES
	  OPEN_LANDS
	  NONE
    }
{{< /mermaid >}}

##### Land Record Type

{{<mermaid align="left">}}
classDiagram
    class Name{
      NONE
	  REVENUE_REGISTRATION
	  PD_ACT
    }
{{< /mermaid >}}

##### Drainage Type

{{<mermaid align="left">}}
classDiagram
    class DrainageType{
      NONE
	  OTHER
	  UNDER_GROUND
	  KACCHA
	  PAKKA
    }
{{< /mermaid >}}
##### Road Type

{{<mermaid align="left">}}
classDiagram
    class RoadType{
      EARTHEN
      GRAVEL
      WBM
      CC
      BT
      NONE
    }
{{< /mermaid >}}


##### Roof Type

{{<mermaid align="left">}}
classDiagram
    class RoofType{
      RCC
      AC_SHEETS_OR_ZINC_SHEETS
      COUNTRY_OR_MANGALORE_TILES
      SHABAD_STONES
      THATCHED_OR_MUD_ROOF
      NONE
    }
{{< /mermaid >}}

##### Construction Type

{{<mermaid align="left">}}
classDiagram
    class ConstructionType{
      COMPLETED
      NOT_COMPLETED
      NONE
    }
{{< /mermaid >}}


#### Feature Permission
|Permission code|Action|
|---------------|-------|
|HOUSE_PROPERTY_CREATE|to Create the House Property|
|HOUSE_PROPERTY_VIEW|to View the House Property|


#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|door_number|


## Acceptance Criteria
|Description|
|-------------|
|Version : 1.0|
|1. Survey User can able to Create, View and Sync the House Property.|

## User Experience


### State Machine

### Sequence Diagram

    

## Unit Test Cases
#### Authorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create |ut_p_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_100 ut_p_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_200 ut_p_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_300 ut_p_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_400 ut_p_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_500 ut_p_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_600 ut_p_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_700 ut_p_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_800 ut_p_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_900 ut_p_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_1000 ut_p_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_1100 ut_p_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_1200 ut_p_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_1300 ut_p_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_1400 ut_n_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_1500 ut_n_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_1600 ut_n_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_1700 ut_n_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_1800 ut_n_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_1900 ut_n_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_2000 ut_n_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_2100 ut_n_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_2200 ut_n_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_2300 ut_n_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_2400 ut_n_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_2500 ut_n_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_2600 ut_n_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_2700 ut_n_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_2800 ut_n_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_2900 ut_n_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_3000 ut_n_c_GSTS_HOUSE_PROPERTY_DATASYNC_API_3100 |**Positive Test Cases:** 1.House Property Data Sync Postive Test Cases with max length Combination-01 2.House Property Data Sync Postive Test Cases with minimum length Combination-02 3.House Property Data Sync Postive Test Cases with minimum length Combination-03 4.House Property Data Sync Postive Test Cases with minimum length Combination-04 5.House Property Data Sync Postive Test Cases with minimum length Combination-05 6.House Property Data Sync Postive Test Cases with minimum length Combination-06 7.House Property Data Sync Postive Test Cases with minimum length Combination-07 8.House Property Data Sync Postive Test Cases with minimum length Combination-08 9.House Property Data Sync Postive Test Cases with minimum length Combination-09 10.House Property Data Sync Postive Test Cases with minimum length Combination-10 11.House Property Data Sync Postive Test Cases with minimum length Combination-11 12.House Property Data Sync Postive Test Cases with minimum length Combination-12 13.House Property Data Sync Positive Test Cases with minimum length Combination-13 14.House Property Data Sync Postive Test Cases with minimum length Combination-14 15.House Property Data Sync Postive Test Cases with maximum length Combination-01 for apartment reg fields 16.House Property Data Sync Postive Test Cases with minimum length Combination-01 for apartment reg fields 17.House Property Data Sync Postive Test Cases with minimum length Combination-02 for apartment reg fields 18.House Property Data Sync Postive Test Cases with minimum length Combination-03 for apartment reg fields **Negative Test Cases:** 1.House Property Data Sync Negative Test Cases with more than max length Combination-15 2.House Property Data Sync Negative Test Cases with without family Combination-16 3.House Property Data Sync Negative Test Cases passing null partitions Combination-17 4.House Property Data Sync Negative Test Cases Without create house Combination-17 5.House Property Data Sync Negative Test Cases with below the minimum length Combination-19 6.House Property Data Sync Negative Test Cases with relations Combination-20 7.House Property Data Sync Negative Test Cases with education status and qualification Combination-20 8.House Property Data Sync Negative Test Cases with Invalid Roof type 9.House Property Data Sync Negative Test Cases with Invalid Plingth length and Plingth breadth for 1st floor 10.House Property Data Sync Positive Test Cases with different religion citizen in same house 11.House Property Data Sync Negative Test Cases with max length Combination-01 12.House Property Data Sync Postive Test Cases with max length Combination-01 13.House Property Data Sync Negative Test Cases with max length Combination-01 14.House Property Data Sync Negative Test Cases with max length Combination-01 15.House Property Data Sync Negative Test Cases with Invalid Inputs in citizen 16.House Property Data Sync Negative Test Cases with Invalid Inputs in NonResident citizen 17.House Property Data Sync Negative Test Cases with Invalid Relation with Head type 18.House Property Data Sync Negative Test Cases with Invalid length and characters combination for apartment reg fields 19.House Property Data Sync Negative Test Cases with Concession type:null and apartmentName:null|**id**: 1.Valid Id **address:** 1.Valid Characters 2.length>6 and length<128 3.null **area:**  1.null 2.Value > 0 **latitude** **longitude** **aid:** 1.Valid characters 2.length=12 3.null **name:** 1.Valid Characters 2.length>3 and length<64 3.null **surname:** 1.Valid Characters 2.length>1 and length<32 3.null **fsname:** 1.Valid Characters 2.length>3 and length<64 3.null **gender** **age** **dob** **mobile:** 1.Valid Characters [starts with 6,7,8,9] 2.length=10 3.null **aadhaarInputType** **surveyEndTime** **surveyStartTime**|18|19|37|housePropertyDataSyncPosTC01, housePropertyDataSyncPosTC02, housePropertyDataSyncPosTC03, housePropertyDataSyncPosTC04, housePropertyDataSyncPosTC05, housePropertyDataSyncPosTC06, housePropertyDataSyncPosTC07, housePropertyDataSyncPosTC08, housePropertyDataSyncPosTC09, housePropertyDataSyncPosTC10, housePropertyDataSyncPosTC11, housePropertyDataSyncPosTC12, housePropertyDataSyncPosTC13, housePropertyDataSyncPosTC14, housePropertyDataSyncNegTC15, housePropertyDataSyncNegTC16, housePropertyDataSyncNegTC17, housePropertyDataSyncNegTC18, housePropertyDataSyncNegTC19, housePropertyDataSyncNegTC20, housePropertyDataSyncNegTC21, housePropertyDataSyncNegTC22, housePropertyDataSyncNegTC23, housePropertyDataSyncNegTC24, housePropertyDataSyncPosTC025, housePropertyDataSyncNegTC026, housePropertyDataSyncNegTC027, housePropertyDataSyncNegTC028, housePropertyDataSyncNegTC029, housePropertyDataSyncNegTC030, housePropertyDataSyncNegTC031, housePropertyDataSyncPosTC0036, housePropertyDataSyncPosTC0037, housePropertyDataSyncPosTC0038, housePropertyDataSyncPosTC0039, housePropertyDataSyncNegTC0040, housePropertyDataSyncNegTC0041|


## Security compliance check
1. Only Survey User should Create, View House Data.


## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the House Property should be provided in the User Manual.

## Feature/Defect list
|Feature/Defect ID|Link|Status|
|----|----|---|
|GS-0003|[GS-0003](https://shadkona.atlassian.net/browse/GS-0003)|Closed|


## References
1. [Spring Security](https://spring.io/projects/spring-security)
1. [Intro to Spring Security Expressions](https://www.baeldung.com/spring-security-expressions)
1. [Spring Security Role Based Access Authorization Example](https://www.journaldev.com/8748/spring-security-role-based-access-authorization-example)

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




 
