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
1. We can Create, Update, View, Delete and Search in the auction property.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|-|-|-|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_auction_property_create|To create the Auction Property|
|uc_auction_property_view|To view the Auction Property |
|uc_auction_property_update|To update the Auction Property|
|uc_auction_property_search|To search in the Auction Property|
|uc_auction_property_delete|To delete in the Auction Property|

#### Model Attributes
| Attribute name         | Mandatory | Default value | Input Allowed Char set Layout/API | KV Database Key            | SQLite Column Definition    | Create | Update | Remove | View | List | Search | Remarks |
|------------------------|-----------|---------------|-----------------------------------|----------------------------|-----------------------------|--------|--------|--------|------|------|--------|---------|
| id                     | YES       | NA            | a-zA-Z0-9, maxlen=128             | NA                         | id String                   | YES    | YES    | YES    | NO   | NO   | NO     ||
| auction_data_id        | YES       | NA            | 0-9, maxlen=12                    | AUCTION_ID_KEY             | auctionDataId String        | YES    | YES    | YES    | YES  | NO   | NO     ||
| auction_name           | YES       | NA            | a-zA-Z /&()0-9, maxlen=64         | AUCTION_NAME_KEY           | auctionName String          | YES    | YES    | YES    | YES  | NO   | NO     ||
| auction_type           | YES       | Choose        | Spinner Values                    | AUCTION_TYPE_KEY           | aucType String              | YES    | YES    | YES    | YES  | YES  | NO     ||
| street                 | YES       | NA            | a-zA-Z0-9,._-(), maxlen=64        | ADDRESS_KEY                | address String              | YES    | YES    | YES    | YES  | NO   | NO     ||
| start_bid              | YES       | NA            | 0-9, maxlen=12                    | START_BID_KEY              | startBid String             | YES    | YES    | YES    | YES  | NO   | NO     ||
| deposit_amount         | YES       | NA            | 0-9, maxlen=12                    | DEPOSIT_AMOUNT_KEY         | depositAmount String        | YES    | YES    | YES    | YES  | NO   | NO     ||
| number_of_installments | YES       | 3             | Spinner Values                    | NUMBER_OF_INSTALLMENTS_KEY | numberOfInstallments String | YES    | YES    | YES    | YES  | NO   | NO     ||
| installment_one        | YES       | NA            | 0-9, maxlen=3                     | INSTALLMENT_ONE_KEY        | installmentOne String       | YES    | YES    | YES    | YES  | NO   | NO     ||
| installment_two        | YES       | NA            | 0-9, maxlen=3                     | INSTALLMENT_TWO_KEY        | installmentTwo String       | YES    | YES    | YES    | YES  | NO   | NO     ||
| installment_three      | YES       | NA            | 0-9, maxlen=3                     | INSTALLMENT_THREE_KEY      | installmentThree String     | YES    | YES    | YES    | YES  | NO   | NO     ||
| installment_four       | YES       | NA            | 0-9, maxlen=3                     | INSTALLMENT_FOUR_KEY       | installmentFour String      | YES    | YES    | YES    | YES  | NO   | NO     ||
| installment_five       | YES       | NA            | 0-9, maxlen=3                     | INSTALLMENT_FIVE_KEY       | installmentFive String      | YES    | YES    | YES    | YES  | NO   | NO     ||
| latitude               | YES       | 0.0           | 0-9.+-, maxlen=24                 | LATITUDE_KEY               | latitude String             | YES    | YES    | YES    | YES  | NO   | NO     ||
| longitude              | YES       | 0.0           | 0-9.+-, maxlen=24                 | LONGITUDE_KEY              | longitude String            | YES    | YES    | YES    | YES  | NO   | NO     ||
| image                  | YES       | NA            | a-zA-Z0-9, maxlen=64              | AUCTION_IMAGE              | image String                | YES    | YES    | YES    | YES  | NO   | NO     ||
| survey_pending         | YES       | Yes           | a-zA-Z0-9, maxlen=128             | SURVEY_PENDING_KEY         | survey_pending Boolean      | NA     | YES    | NA     | YES  | YES  | NO     ||
| survey_start_time      | YES       | NA            | a-zA-Z0-9, maxlen=128             | SURVEY_START_TIME          | survey_start_time String    | YES    | NA     | NA     | YES  | NO   | NO     ||
| survey_end_time        | YES       | NA            | a-zA-Z0-9, maxlen=128             | SURVEY_END_TIME            | survey_end_time String      | YES    | NA     | NA     | YES  | NO   | NO     ||
| aadhaar_input_type     | YES       | OCR           | Spinner Values                    | AADHAAR_INPUT_TYPE_KEY     | aadhaar_input_type String   | YES    | YES    | YES    | YES  | NO   | NO     ||
| aadhar_id              | YES       | NA            | 0-9, maxlen=12                    | NAME_KEY                   | aadhaarId String            | YES    | YES    | YES    | YES  | YES  | NO     ||
| name                   | YES       | NA            | a-z A-Z, maxlen=32                | NAME_KEY                   | name String                 | YES    | YES    | YES    | YES  | NO   | NO     ||
| surname                | YES       | NA            | a-zA-Z /, maxlen=64               | SURNAME_KEY                | surname String              | YES    | YES    | YES    | YES  | NO   | NO     ||
| fsname                 | YES       | NA            | a-z A-Z, maxlen=64                | FATHER_SPOUSE_NAME_KEY     | fsname String               | YES    | YES    | YES    | YES  | NO   | NO     ||
| mobile                 | YES       | NA            | 0-9, maxlen=10                    | MOBILE_KEY                 | mobile String               | YES    | YES    | YES    | YES  | NO   | NO     ||
| gender                 | YES       | Male          | Radio Button Values               | GENDER_KEY                 | gender String               | YES    | YES    | YES    | YES  | NO   | NO     ||
| dob                    | YES       | NA            | 0-9 /, maxlen=3                   | DATE_OF_BIRTH_KEY          | dob String                  | YES    | YES    | YES    | YES  | NO   | NO     ||
| age                    | YES       | NA            | 0-9, maxlen=3                     | AGE_KEY                    | age String                  | YES    | YES    | YES    | YES  | NO   | NO     ||
| end_bid                | YES       | NA            | 0-9, maxlen=8                     | END_BID_KEY                | endBid String               | YES    | YES    | YES    | YES  | NO   | NO     ||
| auction_date           | YES       | NA            | a-zA-Z0-9./-@#&amp;_,:, maxlen=32 | AUCTION_DATE_KEY           | auctionDate String          | YES    | YES    | YES    | YES  | NO   | NO     ||
| tax_start_date         | YES       | None          | 0-9 -, maxlen=16                  | AUCTION_TAX_START_DATE_KEY | taxStartdate String         | YES    | YES    | YES    | YES  | NO   | NO     ||
| tax_end_date           | YES       | NA            | 0-9, maxlen=10                    | AUCTION_TAX_END_DATE_KEY   | taxEndDate String           | YES    | YES    | YES    | YES  | NO   | NO     ||
| survey_pending         | YES       | Yes           | 0(No), 1(Yes)                     | SURVEY_PENDING_KEY         | survey_pending Boolean      | NA     | YES    | NA     | YES  | YES  | NO     ||
| dataSync               | YES       | NA            | 0(No), 1(Yes)                     | NA                         | dataSync Boolean            | NA     | NA     | NA     | NO   | NO   | NO     ||
| unlockId               | YES       | NA            | a-zA-Z0-9, maxlen=128             | AUCTION_PROPERTY_UNLOCK_ID | unlockId String             | YES    | NA     | NA     | NO   | NO   | NO     ||
| response_error_msg     | YES       | NA            | a-zA-Z0-9, maxlen=64              | NA                         | responseErrorMsg String     | NO     | NA     | NA     | YES  | NO   | NO     ||
| is_encrypted           | YES       | NA            | 0(No), 1(Yes)                     | NA                         | is_encrypted Boolean        | NA     | NA     | NA     | NO   | NO   | NO     ||



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
### Listing Page
{{<mermaid align="left">}}
graph LR
    Add[+ Add Item]-->Search[Search box]-->BackButton[<- Back]   
{{< /mermaid >}}
### Form Page
{{<mermaid align="left">}}
graph LR
    Next[NEXT]-->BackButton[<- Back]
{{< /mermaid >}}
### View Page
{{<mermaid align="left">}}
graph LR
    Finish[FINISH]-->ShowOnMap[SHOW ON MAP]-->BackButton[<- Back]
{{< /mermaid >}}
### List to View Page
{{<mermaid align="left">}}
graph LR
    Edit[EDIT]-->ShowOnMap[SHOW ON MAP]-->BackButton[<- Back]
{{< /mermaid >}}

### State Machine
{{<mermaid align="left">}}
flowchart TD
	SurveyItemsPage[Survey Dashboard] 
	ListPage((Auction Property List Page))
	FromPage[Auction Form Page]
	ConfirmationPage[Auction Confirmation Page]
    ViewPage[Auction View Page]
	Start((Start))
    AddBtn[Add Item Button]
    NextBtn1[Next Button]
    FinishBtn1[Finish Button]
    EditBtn[Edit Button]
    BackBtn1[Back Button]
    AuctionProperty[Auction Property]	
    AuctionDelteItem[Auction Item]
    DeleteAuctionMessage>Auction Property Deleted]
    End((end))
    ErrorPage>Exception Message]
    Start-->SurveyItemsPage
    subgraph Taxable Properties
        SurveyItemsPage--C-->AuctionProperty
	end
    subgraph Error
        AuctionProperty--F-->ErrorPage
        ErrorPage-->End
	end	
	subgraph List Page
        AuctionProperty--S-->ListPage
        ListPage--C-->AddBtn
        ListPage--C-->AuctionItem
        ListPage--SAD-->AuctionDelteItem
        AuctionDelteItem--F-->ListPage
	end
    subgraph Form Page
        AddBtn--S-->FromPage
        AddBtn--F-->ListPage
        FromPage--C-->NextBtn1
	end
	subgraph Details View Page
        NextBtn1--F-->FromPage
        NextBtn1--S-->ConfirmationPage
        ConfirmationPage--C-->FinishBtn1
        FinishBtn1--F-->ConfirmationPage
        FinishBtn1--S-->ListPage
        ConfirmationPage--C-->BackBtn1
        BackBtn1--S-->FromPage
        BackBtn1--F-->ConfirmationPage
	end
	subgraph View Page
        AuctionItem--S-->ViewPage
        AuctionItem--F-->ListPage
        ViewPage--C-->EditBtn
        EditBtn--F-->ViewPage
        EditBtn--S-->FromPage
	end
	subgraph delete
	    AuctionDelteItem--S-->DeleteAuctionMessage
	end
	%%For click Repressentation
	linkStyle 1 stroke:blue,stroke-width:2px;
	linkStyle 5 stroke:blue,stroke-width:2px;
	linkStyle 6 stroke:blue,stroke-width:2px;
	linkStyle 11 stroke:blue,stroke-width:2px;
	linkStyle 14 stroke:blue,stroke-width:2px;
	linkStyle 17 stroke:blue,stroke-width:2px;
	linkStyle 22 stroke:blue,stroke-width:2px;
	%%For success Representation
	linkStyle 4 stroke:green,stroke-width:2px;
	linkStyle 9 stroke:green,stroke-width:2px;
	linkStyle 13 stroke:green,stroke-width:2px;
	linkStyle 16 stroke:green,stroke-width:2px;
	linkStyle 18 stroke:green,stroke-width:2px;
	linkStyle 20 stroke:green,stroke-width:2px;
	linkStyle 24 stroke:green,stroke-width:2px;
	linkStyle 25 stroke:green,stroke-width:2px;
	%%For failure Representation
	linkStyle 2 stroke:red,stroke-width:2px;
	linkStyle 8 stroke:red,stroke-width:2px;
	linkStyle 10 stroke:red,stroke-width:2px;
	linkStyle 12 stroke:red,stroke-width:2px;
	linkStyle 15 stroke:red,stroke-width:2px;
	linkStyle 19 stroke:red,stroke-width:2px;
	linkStyle 21 stroke:red,stroke-width:2px;
	linkStyle 23 stroke:red,stroke-width:2px;
	%%For delete Representation
	linkStyle 7 stroke:orange,stroke-width:2px;
	
{{< /mermaid >}}
|Symbol|Action|
|------|------|
|C|ClickOn|
|S|OnSuccess|
|F|OnFailure|
|SAD|Swap And Delete|
|Blue Link|Click|
|Green Link|Success|
|Red Link|Failure|
|Orange Link|Delete|


### Flowchart
{{<mermaid align="center">}}
%%{init: {'themeVariables': {'edgeLabelBackground':'#FFFF', 'tertiaryColor': '#fff0f0'}}}%%
flowchart
    Start((start))
    End((end))
    SurveyDashboard[Survey Dashboard]
    ListPage[Auction Listing Page]
    subgraph List Page
        DBCallLoadAllAuctions[loadAllAuctions From SQLite DB]
        SetAuctionsDatainListPage[Set Auction Data in List Page]
    end
    subgraph Add Item
        FormPage[Auction Form Page]
    end 
    subgraph Form Page
        FormPageInitialSetUp[Auction From Page Initial SetUp]
        saveDatainKVDatabase[save Form Data in KvDataBase]
        DataValidationCehck{Data Validation}
        DetailsConfirmationPage[Auction Details Confirmation Page]
        ShowMessageDataValidation>Show Message: Please Enter Valid Data]
    end
    subgraph Details Confirmation Page
        getDataFromKVDatabase[get Auction KV Data From KV Database]
        setDataInConfirmationPage[set Auction Data in Confirmation Page]
        PrepareAuctionObject[ Auction Object Preparation]
        DBCallInsertOrUpdateAuctionData[Insert / Update Auction Object in SQLite DB]
    end       
    subgraph View Page
        FetchAuctionByID[fetchAuctionById From SQLite DB]
        setDataInViewPage[set Auction Data in Veiw Page]
    end    
    Start-->SurveyDashboard
    SurveyDashboard--Click Auction-->ListPage
    %%List page
    ListPage-->DBCallLoadAllAuctions
    DBCallLoadAllAuctions-->SetAuctionsDatainListPage
    %%Add Auction
    ListPage--Add Auction-->FormPage
    FormPage-->FormPageInitialSetUp
    FormPageInitialSetUp--Input Auction Data-->saveDatainKVDatabase
    saveDatainKVDatabase-->DataValidationCehck
    DataValidationCehck--Valid-->DetailsConfirmationPage
    DataValidationCehck--Not Valid-->ShowMessageDataValidation
    %%Details Confirmation Page
    DetailsConfirmationPage-->getDataFromKVDatabase
    getDataFromKVDatabase-->setDataInConfirmationPage
    setDataInConfirmationPage-->PrepareAuctionObject
    PrepareAuctionObject-->DBCallInsertOrUpdateAuctionData
    DBCallInsertOrUpdateAuctionData-->DBCallLoadAllAuctions
    %%Edit Auction
    ListPage--View Auction-->FetchAuctionByID
    FetchAuctionByID-->setDataInViewPage
    setDataInViewPage--Edit-->FormPage
    ListPage-->End
{{< /mermaid >}}


### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant SQLite as SQLite Database
    participant ListPage as Auction Listing Page
    participant FormPage as Auction Form Page
    participant KVDB as KV Database
    participant ViewPage as Auction View Page
    autonumber 
       
    rect rgb(244,244,244)
        ListPage->>+SQLite: load All Auction
        SQLite-->>-ListPage: List Of Auction
    end
    
    rect rgb(244,244,244)
        Note right of FormPage: If (Adding new Auction Property) (3) else { (7) } 
        FormPage->>+KVDB: save Auction KV Data in KVDatabase
    end
    
    rect rgb(244,244,244)
        ViewPage->>+KVDB: get Auction KV Data 
        KVDB-->>-ViewPage: KV Aucttion Data    
    end  
    rect rgb(244,244,244)
        Note Left of ViewPage: if (Edit == true) {update update Auction} else {insert Auction}
        ViewPage->>+SQLite: updateAuction(auction) (or) insertAuction(auction) 
    end  
    rect rgb(244,244,244)
        Note right of SQLite: Repeat (1) and (2)
    end
    rect rgb(244,244,244)
        Note left of ViewPage: View Auction Data
        ViewPage->>+SQLite: fetchAuctionById(id) 
        SQLite-->>-ViewPage: Auction Object
    end   
    rect rgb(244,244,244)
        Note left of ViewPage: Edit Auction Data
        FormPage->>+SQLite: fetchAuctionById(id) 
        SQLite-->>-FormPage: Auction Object
    end    
    rect rgb(244,244,244)
        Note right of FormPage: Repeat (3) to (6)
    end
    rect rgb(244,244,244)
        Note right of SQLite: Repeat (1) and (2)
    end    
        
          
{{< /mermaid >}}

## Acceptance Criteria
|Description|
|-------------|
|Version : 1.0|
|1. Survey User can able to Create, View, Update, Search, Delete and Sync the Auction Property.|
## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
|-|-|-|
|-|-|-|

## Security compliance check
1. Only Survey User should Create, View, Update, Delete, Search and Sync the Auction Property.
 

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




 
