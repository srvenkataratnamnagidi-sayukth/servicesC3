---
title: TradeLicense Property
tags : ["Composing"]
---

## Introduction
TradeLicense Property is one of the features of the software product which contains the data of all the TradeLicense properties in the Telangana state.  A trade license is a document/certificate that gives the permission to the applicant (person seeking to open a business) to commence a particular trade or business in a particular area/location.
By using this TradeLicense property feature, Survey User can store every Trade License property in the panchayat.

## Business Assumptions
1. TradeLicense Property feature should be planned at the design phase.
1. User should be in the panchayat level to create the TradeLicense property.
1. Owner Aadhaar details are required to create the TradeLicense property.
1. Survey User can able to sync the TradeLicense property to GS-Cloud.

## Requirements
### Functional Requirements
1. To create TradeLicense Property Survey User should complete Panchayat Selection process. 
1. Only one TradeLicense property is allowed with the same name.
1. Only one TradeLicense property is allowed with the same License Number.
1. Once TradeLicense property synced, user not allowed to update it.

### Non-functional Requirements
1. Multiple users can create TradeLicense property in the same panchayat.
1. Multiple users can create same TradeLicense property in the same panchayat. But only one TradeLicense Property will sync among all users based on who sync first.
1. One citizen can have multiple TradeLicense properties in the same panchayat or different panchayats.

### Problem Statement
TradeLicense Property feature is required to store all the TradeLicense property details in the panchayat level.

### Design 
1. Each TradeLicense property has an Aadhaar Input Type, owner's Aadhaar number, Name, Surname, Father/Spouse Name, Mobile Number, Gender, Date Of Birth, Age, TradeLicense Name, Trade Category, Street Name, GP Sanction Id, Annual Turnover, Motor Capacity, Latitude, Longitude, and Survey Pending Status fields.
1. Survey User can Create, View the TradeLicense property.
1. Only one TradeLicense property is allowed with the same name.
1. Only one TradeLicense property is allowed with the same License Number.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Start / Continue Survey|[Start / Continue Survey]({{< ref "StartOrContinueSurvey" >}})|Parent Page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_trade_license_property_create|To create the TradeLicense property|
|uc_trade_license_property_view|To view the TradeLicense property|


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

##### TradeLicense Category

{{<mermaid align="left">}}
classDiagram
    class TradeLicenseCategory{
      AGRO_CENTER
          ANIMAL_FEED
          AUTO_MOBILES
          BAKERY
          BOOKSTORE
          BRICKWORK
          CEMENT_SHOP
          CLOTH_SHOWROOM
          COMPUTER_CENTER
          COOL_DRINKS
          CRACKERS
          CYCLE_SHOP
          EGG_MART
          ELECTRICAL_ELECTRONICS
          EMPORIUM
          ENTERPRISE
          HOSTELS
          HOTELS
          TEA_STALL
          DHABHA
          RICE_MILL
          INSTITUTE
          JEWELLERY
          KIRANA_GENERAL_STORE
          LODGE
          MEAT_CHICKEN_CENTER
          MEDICAL_STORE
          METAL_BRASS_ITEMS
          MILK_PARLOUR
          MILLS
          MOTOR_HP_BASED
          MUSICAL_SHOW_ROOM
          NET_CAFE
          OILS_PULSES
          OPTICAL_SHOWROOM
          PAINT_SHOP
          PAN_SHOP
          PETROL_BUNK
          PHOTO_STUDIO
          PLASTIC_ITEM_SHOP
          POULTRY_FORM
          PRINTING_PRESS
          REPAIRING_SHOP
          RICE_BOILERS
          STALLS
          STEEL_ITEMS
          SWEET_SHOP
          TAILORING_SHOP
          TENT_HOUSE
          THEATRES
          TILES_SANITORY
          TIMBER_SHOP
          TOY_SHOP
          TRADER_AGENCIES
          TRANSPORT
          VEGETABLES
          FRUITS
          WHOLESALE_MANDI
          WINE_SHOP
          WORKSHOP_LAZER
          XEROX_SHOP
          CELLPHONE_SHOP
          FISH_PRAWN_SHOP
          BAJJI_SHOP
          FRUIT_JUICE_SHOP
          BEAUTY_PARLOUR
          BARBER_SHOP
          GYM
          FERTILIZERS_PESTICIDES
          FINANCE
          FOOTWARE
          GAS_AGENCY
          GENERAL_STORES
          HARDWARE_SHOWROOM
          CELL_TOWER
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
|Unique Keys|1. trade_name|
||2. license_number|

## Acceptance Criteria
|Description|
|-------------|
|Version : 1.0|
|1. Survey User can able to Create, View and Sync the TradeLicense Property.|

## User Experience


### State Machine

### Flowchart


### Sequence Diagram


## Unit Test Cases
#### Authorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create |ut_p_c_GSTS_TRADE_PROPERTY_DATASYNC_API_100 ut_n_c_GSTS_TRADE_PROPERTY_DATASYNC_API_200 ut_n_c_GSTS_TRADE_PROPERTY_DATASYNC_API_300 |**Positive Test Cases:** TradeLicense Data Sync Postive Test Cases Combination-01 **Negative Test Cases:** 1.TradeLicense Data Sync Negative Test Cases Combination-02 2.TradeLicense Data Sync Negative Test Case - create TradeProperty without DB Connection |**id**: 1.Valid Id **tradeAddress:** 1.Valid Characters 2.length>6 and length<128 3.null **tradeCategory** **tradeName:** 1.Valid Characters 2.length>3 and length<64 3.null **turnover:**  1.null 2.Value > 0 **licenceNumber:** 1.Valid Characters 2.length>=3 and length<=64 3.null 4. unique **motorCapacity:** Enum Values: 0L,1L,5L,10L,25L,50L,100L **latitude** **longitude** **aid:** 1.Valid characters 2.length=12 3.null **name:** 1.Valid Characters 2.length>3 and length<64 3.null **surname:** 1.Valid Characters 2.length>1 and length<32 3.null **fsname:** 1.Valid Characters 2.length>3 and length<64 3.null **gender** **age** **dob** **mobile:** 1.Valid Characters [starts with 6,7,8,9] 2.length=10 3.null **aadhaarInputType** **surveyEndTime** **surveyStartTime**|79|8|87|tradeLicensePropertyDataSyncPosTC01, tradeLicensePropertyDataSyncNegTC02, tradeLicensePropertyDataSyncNegTC03 |
|1.0| View |ut_n_v_GSTS_TRADE_PROPERTY_DATASYNC_API_400|**Negative Test Cases:** TradeLicense Data Sync Negative Test Cases - View TradeProperty Without DB Connection|1.Valid Id|0|1|1|tradeLicensePropertyDataSyncNegTC04|

## Security compliance check
1. Only Survey User should Create, View and Sync the TradeLicense Property.

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




 
