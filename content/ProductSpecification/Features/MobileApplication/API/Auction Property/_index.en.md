---
title: Auction Property
tags : ["Composing"]
---

## Introduction
Auction Property is one of the basic features of the software product which contains the data of all the
auction properties in the Telangana state.Some properties of the panchayat given lease to the people by auction.By using this auction property feature we have to store every
 auction property data and know about every auction property in the state. Every auction property should 
 be stored under respective panchayat only. Auction property will be created based on auction asset.

## Business Assumptions
1. Auction Property feature should be planned at the design phase.
1. User should be in the panchayat level to create the auction property.
1. Owner Aadhaar number is required to create the auction property.
1. Survey User can able to sync the Auction Property to GS-Cloud

## Requirements
### Functional Requirements
1. Auction Property feature only accessible in panchayat level.
1. While creating auction property, the owner's aadhaar number will bind to it.
1. Atleast one Auction Asset is required to create the auction property.
1. Only one auction property should be allowed to create for single auction asset.
1.After Auction Property synced, User not allowed to update it.


### Non-functional Requirements
1. Multiple users can create the auction property in the same panchayat.
1. One citizen can have multiple auction properties in the same panchayat or different panchayats.

### Problem Statement
Auction Property feature is required to store all the auction property details in the panchayat level.

### Design 
1. Each Auction property has a owner Aadhaar number, Tax StartDate, Tax EndDate, Auction Data, Auction Date 
and End bid.
1. We can Create, and View in the auction property.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|-|-|-|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_auction_property_create|To create the Auction Property|
|uc_auction_property_view|To view the Auction Property |

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


##### Auction Category

{{<mermaid align="left">}}
classDiagram
    class AuctionCategory{
      NONE
      AGRICULTURE_LAND
      BANDELA_DODDI
      CATTLE_SHED
      DAILY_MARKET
      FERRY
      FISHING_RIGHTS
      FISHING_PONDS
      GREEN_GRASS
      KABELA
      OLD_CONDEMNED_ITEMS
      SHOPPING_MALLS
      TREE
      WEAKLY_MARKET
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
|Unique Keys|auction_name|

## User Experience

### State Machine



### Flowchart

### Sequence Diagram

## Acceptance Criteria
|Description|
|-------------|
|Version : 1.0|
|1. Survey User can able to Create, View, and Sync the Auction Property.|

## Unit Test Cases
#### Authorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create |ut_p_c_GSTS_AUCTION_PROPERTY_DATASYNC_API_100 ut_n_c_GSTS_AUCTION_PROPERTY_DATASYNC_API_200 ut_n_c_GSTS_AUCTION_PROPERTY_DATASYNC_API_300 ut_n_c_GSTS_AUCTION_PROPERTY_DATASYNC_API_400 |**Positive Test Cases:** Auction Property Data Sync Postive Test Cases Combination-01 **Negative Test Cases:** 1.Auction Property Data Sync Negative Test Cases Combination-02 2.Auction Property Data Sync Negative Test Cases- Create Auction without DB Connection 3.Auction Property Data Sync Negative Test Cases- Create Auction without DB Connection| **Auction Data**  **id**: 1.Valid Id **address:** 1.Valid Characters 2.length>6 and length<128 3.null **auctionName**: 1.Valid Characters 2.length>3 and length<64 3.null **auctionType** **depositAmount:** 1.null 2.Value > 0 **installmentOne** **installmentTwo** **installmentThree** **installmentFour** **installmentFive** **latitude** **longitude** **numberOfInstallments** **startBid:**  1.null 2.Value > 0 **Auction Property** **id:** 1.Valid Id **auctionDataId:** 1.Valid Id **auctionDate** **endBid:**  1.null 2.Value > 0 **taxEndDate** **taxStartdate** **aadhaarId:** 1.Valid characters 2.length=12 3.null **name:** 1.Valid Characters 2.length>3 and length<64 3.null **surname:** 1.Valid Characters 2.length>1 and length<32 3.null **fsname:** 1.Valid Characters 2.length>3 and length<64 3.null **gender** **age** **dob** **mobile:** 1.Valid Characters [starts with 6,7,8,9] 2.length=10 3.null **aadhaarInputType** **surveyEndTime** **surveyStartTime**|15|15|30|auctionPropertyDataSyncPosTC01, auctionPropertyDataSyncNegTC02, auctionPropertyDataSyncNegTC03, auctionPropertyDataSyncNegTC04|
|1.0| View |ut_n_v_GSTS_AUCTION_PROPERTY_DATASYNC_API_500|**Negative Test Cases:** 1.Auction Property Data Sync Negative Test Cases- View AuctionProperty without DB Connection|1.Valid Id|0|1|1|auctionPropertyDataSyncNegTC05|

## Security compliance check
1. Only Survey User should Create, View and Sync the Auction Property.
 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the USER PERMISSIONs in the User Manual. It's scope is limited to Developer Technical Documentation

## Feature/Defect list
|Feature/Defect ID|Link|Status|
|----|----|---|
|GS-0002|[GS-0002](https://shadkona.atlassian.net/browse/GS-0002)|Closed|


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




 
