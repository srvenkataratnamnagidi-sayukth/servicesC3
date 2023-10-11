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
1. Each Advertisement property has Advertisement Name, Street Name, Board Size, GP Sanction Id, Advertisement Category,Advertisement Asset, Number Of Installments fields.
1. Survey User can Create, View, Update, Delete and search in the Advertisement Property.
1. Only one Advertisement Property is allowed with the same name.

#### Dependant Features
| Feature name            | Reference Link                                                 | Remarks     |
|-------------------------|----------------------------------------------------------------|-------------|
| Start / Continue Survey | [Start / Continue Survey]({{< ref "StartOrContinueSurvey" >}}) | Parent Page |

#### Use cases
| Use case Code                    | Description                          |
|----------------------------------|--------------------------------------|
| uc_advertisement_property_create | To create the Advertisement Property |
| uc_advertisement_property_view   | To view the Advertisement Property   |
| uc_advertisement_property_update | To update the Advertisement Property |
| uc_advertisement_property_search | To search the Advertisement Property |
| uc_advertisement_property_delete | To delete the Advertisement Property |


#### Model Attributes
| Attribute name         | Mandatory | Default value | Input Allowed Char set Layout/API | KV Database Key                  | SQLite Column Definition    | Create | Update | Remove | View | List | Search | Remarks |
|------------------------|-----------|---------------|-----------------------------------|----------------------------------|-----------------------------|--------|--------|--------|------|------|--------|---------|
| id                     | YES       | NA            | a-zA-Z0-9, maxlen=128             | NA                               | id String                   | YES    | YES    | YES    | NO   | NO   | NO     ||
| aadhaar_input_type     | YES       | OCR           | Spinner Values                    | AADHAAR_INPUT_TYPE_KEY           | aadhaar_input_type String   | YES    | YES    | YES    | YES  | NO   | NO     ||
| aid                    | YES       | NA            | 0-9, maxlen=12                    | AADHAR_NUMBER_KEY                | aid String                  | YES    | YES    | YES    | YES  | NO   | NO     ||
| name                   | YES       | NA            | a-zA-Z, maxlen=64                 | NAME_KEY                         | name String                 | YES    | YES    | YES    | YES  | YES  | NO     ||
| surname                | YES       | NA            | a-z A-Z, maxlen=32                | SURNAME_KEY                      | surname String              | YES    | YES    | YES    | YES  | NO   | NO     ||
| fsname                 | YES       | NA            | a-zA-Z /, maxlen=64               | FATHER_NAME_KEY                  | fsname String               | YES    | YES    | YES    | YES  | NO   | NO     ||
| mobile                 | YES       | NA            | 0-9, maxlen=10                    | MOBILE_NUMBER_KEY                | mobile String               | YES    | YES    | YES    | YES  | YES  | NO     ||
| gender                 | YES       | Male          | Radio Button Values               | GENDER_KEY                       | gender String               | YES    | YES    | YES    | YES  | NO   | NO     ||
| dob                    | YES       | NA            | 0-9/-, maxlen=10                  | DATEOFBIRTH_KEY                  | dob String                  | YES    | YES    | YES    | YES  | NO   | NO     ||
| age                    | YES       | NA            | 0-9, maxlen=3                     | AGE_KEY                          | age String                  | YES    | YES    | YES    | YES  | NO   | NO     ||
| advertisementName      | YES       | NA            | a-zA-Z0-9.@$_#,:;()/\, maxlen=64  | ADVERTISEMENT_NAME_KEY           | advertisementName String    | YES    | YES    | YES    | YES  | YES  | NO     ||
| board_location         | YES       | None          | a-zA-Z0-9, maxlen=128             | BOARD_LOCATION_KEY               | boardLocation String        | YES    | YES    | YES    | YES  | YES  | NO     ||
| board_size             | YES       | NA            | 0-9                               | BOARD_SIZE_KEY                   | boardSize String            | YES    | YES    | YES    | YES  | NO   | NO     ||
| gp_sanction_id         | YES       | NA            | a-zA-Z0-9.@$_#,:;()/\,, maxlen=10 | GP_SANCTION_ID_KEY               | gpSanctionId String         | YES    | YES    | YES    | YES  | NO   | NO     ||
| category               | YES       | Choose        | Spinner Values                    | CATEGORY_KEY                     | category String             | YES    | YES    | YES    | YES  | YES  | NO     ||
| asset_type             | YES       | Choose        | Spinner Values                    | ASSERT_TYPE_KEY                  | assetType String            | YES    | YES    | YES    | YES  | NO   | NO     ||
| number_of_installments | YES       | 1             | Spinner Values                    | NO_OF_INSTALLMENTS_KEY           | numberOfInstallments String | YES    | YES    | YES    | YES  | NO   | NO     ||
| latitude               | YES       | 0.0           | 0-9.+-, maxlen=24                 | LATITUDE_KEY                     | latitude String             | YES    | YES    | YES    | YES  | NO   | NO     ||
| longitude              | YES       | 0.0           | 0-9.+-, maxlen=24                 | LONGITUDE_KEY                    | longitude String            | YES    | YES    | YES    | YES  | NO   | NO     ||
| image                  | YES       | NA            | a-zA-Z0-9, maxlen=128             | NA                               | image String                | YES    | YES    | YES    | YES  | NO   | NO     ||
| dataSync               | YES       | NA            | 0(No), 1(Yes)                     | NA                               | dataSync Boolean            | NA     | NA     | NA     | NO   | NO   | NO     ||
| imageSync              | YES       | NA            | 0(No), 1(Yes)                     | NA                               | imageSync Boolean           | NA     | NA     | NA     | NO   | NO   | NO     ||
| survey_pending         | YES       | Yes           | 0(No), 1(Yes)                     | SURVEY_PENDING_KEY               | survey_pending Boolean      | NA     | YES    | NA     | YES  | YES  | NO     ||
| survey_start_time      | YES       | NA            | a-zA-Z0-9, maxlen=128             | SURVEY_START_TIME                | survey_start_time String    | YES    | NA     | NA     | YES  | NO   | NO     ||
| survey_end_time        | YES       | NA            | a-zA-Z0-9, maxlen=128             | SURVEY_END_TIME                  | survey_end_time String      | YES    | NA     | NA     | YES  | NO   | NO     ||
| avgSurveyTime          | YES       | NA            | a-zA-Z0-9, maxlen=128             | SURVEY_TIME                      | avgSurveyTime String        | YES    | NA     | NA     | YES  | NO   | NO     ||
| property_locked_id     | YES       | NA            | a-zA-Z0-9, maxlen=128             | ADVERTISEMENT_PROPERTY_UNLOCK_ID | property_locked_id String   | YES    | NA     | NA     | NO   | NO   | NO     ||
| response_error_msg     | YES       | NA            | a-zA-Z0-9, maxlen=NA              | NA                               | responseErrorMsg String     | NO     | NA     | NA     | YES  | NO   | NO     ||
| is_encrypted           | YES       | NA            | 0(No), 1(Yes)                     | NA                               | is_encrypted Boolean        | NA     | NA     | NA     | NO   | NO   | NO     ||


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
| Permission code | Action |
|-----------------|--------|
| -               | -      |
| -               | -      |


#### Constraints
| Constraint  | Key                                     |
|-------------|-----------------------------------------|
| Primary Key | id                                      |
| Unique Keys | 1. gp_sanction_id 2. advertisement_name |

## Acceptance Criteria
| Description                                                                                          |
|------------------------------------------------------------------------------------------------------|
| Version : 1.0                                                                                        |
| 1. Survey User can able to Create, View, Update, Search, Delete and Sync the Advertisement Property. |

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
	ListPage((Advertisement Property List Page))
	FromPage[Advertisement Form Page]
	ConfirmationPage[Advertisement Confirmation Page]
    AdvertisementItem[Advertisement Item]
    ViewPage[Advertisement View Page]
	Start((Start))
    AddBtn[Add Item Button]
    NextBtn1[Next Button]
    FinishBtn1[Finish Button]
    EditBtn[Edit Button]
    BackBtn1[Back Button]
    AdvertisementProperty[Advertisement Property]	
    AdvertisementDelteItem[Advertisement Item]
    DeleteAdvertisementMessage>Advertisement Property Deleted]
    End((end))
    ErrorPage>Exception Message]
    Start-->SurveyItemsPage
    subgraph Taxable Properties
        SurveyItemsPage--C-->AdvertisementProperty
	end
    subgraph Error
        AdvertisementProperty--F-->ErrorPage
        ErrorPage-->End
	end	
	subgraph List Page
        AdvertisementProperty--S-->ListPage
        ListPage--C-->AddBtn
        ListPage--C-->AdvertisementItem
        ListPage--SAD-->AdvertisementDelteItem
        AdvertisementDelteItem--F-->ListPage
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
        AdvertisementItem--S-->ViewPage
        Advertisementtem--F-->ListPage
        ViewPage--C-->EditBtn
        EditBtn--F-->ViewPage
        EditBtn--S-->FromPage
	end
	subgraph delete
	    AdvertisementDelteItem--S-->DeleteAdvertisementMessage
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

| Symbol      | Action          |
|:------------|:----------------|
| C           | ClickOn         |
| S           | OnSuccess       |
| F           | OnFailure       |
| SAD         | Swap And Delete |
| Blue Link   | Click           |
| Green Link  | Success         |
| Red Link    | Failure         |
| Orange Link | Delete          |

### Flowchart
{{<mermaid align="center">}}
%%{init: {'themeVariables': {'edgeLabelBackground':'#FFFF', 'tertiaryColor': '#fff0f0'}}}%%
flowchart
    Start((start))
    End((end))
    SurveyDashboard[Survey Dashboard]
    ListPage[Advertisement Listing Page]
    subgraph List Page
        DBCallLoadAllAdvertisements[loadAllAdvertisements From SQLite DB]
        SetAdvertisementsDatainListPage[Set Advertisement Data in List Page]
    end
    subgraph Add Item
        FormPage[Advertisement Form Page]
    end 
    subgraph Form Page
        FormPageInitialSetUp[Advertisement From Page Initial SetUp]
        saveDatainKVDatabase[save Form Data in KvDataBase]
        DataValidationCehck{Data Validation}
        DetailsConfirmationPage[Advertisement Details Confirmation Page]
        ShowMessageDataValidation>Show Message: Please Enter Valid Data]
    end
    subgraph Details Confirmation Page
        getDataFromKVDatabase[get Advertisement KV Data From KV Database]
        setDataInConfirmationPage[set Advertisement Data in Confirmation Page]
        PrepareAdvertisementObject[ Advertisement Object Preparation]
        DBCallInsertOrUpdateAdvertisementData[Insert / Update Advertisement Object in SQLite DB]
    end       
    subgraph View Page
        FetchAdvertisementByID[fetchAdvertisementById From SQLite DB]
        setDataInViewPage[set Advertisement Data in Veiw Page]
    end    
    Start-->SurveyDashboard
    SurveyDashboard--Click Advertisement-->ListPage
    %%List page
    ListPage-->DBCallLoadAllAdvertisements
    DBCallLoadAllAdvertisements-->SetAdvertisementsDatainListPage
    %%Add Advertisement
    ListPage--Add Advertisement-->FormPage
    FormPage-->FormPageInitialSetUp
    FormPageInitialSetUp--Input Advertisement Data-->saveDatainKVDatabase
    saveDatainKVDatabase-->DataValidationCehck
    DataValidationCehck--Valid-->DetailsConfirmationPage
    DataValidationCehck--Not Valid-->ShowMessageDataValidation
    %%Details Confirmation Page
    DetailsConfirmationPage-->getDataFromKVDatabase
    getDataFromKVDatabase-->setDataInConfirmationPage
    setDataInConfirmationPage-->PrepareAdvertisementObject
    PrepareAdvertisementObject-->DBCallInsertOrUpdateAdvertisementData
    DBCallInsertOrUpdateAdvertisementData-->DBCallLoadAllAdvertisements
    %%Edit Advertisement
    ListPage--View Advertisement-->FetchAdvertisementByID
    FetchAdvertisementByID-->setDataInViewPage
    setDataInViewPage--Edit-->FormPage
    ListPage-->End
{{< /mermaid >}}

### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant SQLite as SQLite Database
    participant ListPage as Advertisement Listing Page
    participant FormPage as Advertisement Form Page
    participant KVDB as KV Database
    participant ViewPage as Advertisement View Page
    autonumber 
       
    rect rgb(244,244,244)
        ListPage->>+SQLite: load All Advertisement
        SQLite-->>-ListPage: List Of Advertisement
    end
    
    rect rgb(244,244,244)
        Note right of FormPage: If (Adding new Advertisement Property) (3) else { (7) } 
        FormPage->>+KVDB: save Advertisement KV Data in KVDatabase
    end
    
    rect rgb(244,244,244)
        ViewPage->>+KVDB: get Advertisement KV Data 
        KVDB-->>-ViewPage: KV Advertisement Data    
    end  
    rect rgb(244,244,244)
        Note Left of ViewPage: if (Edit == true) {update update Advertisement} else {insert Advertisement}
        ViewPage->>+SQLite: updateAdvertisement(Advertisement) (or) insertAdvertisement(Advertisement) 
    end  
    rect rgb(244,244,244)
        Note right of SQLite: Repeat (1) and (2)
    end
    rect rgb(244,244,244)
        Note left of ViewPage: View Advertisement Data
        ViewPage->>+SQLite: fetchAdvertisementById(id) 
        SQLite-->>-ViewPage: Advertisement Object
    end   
    rect rgb(244,244,244)
        Note left of ViewPage: Edit Advertisement Data
        FormPage->>+SQLite: fetchAdvertisementById(id) 
        SQLite-->>-FormPage: Advertisement Object
    end    
    rect rgb(244,244,244)
        Note right of FormPage: Repeat (3) to (6)
    end
    rect rgb(244,244,244)
        Note right of SQLite: Repeat (1) and (2)
    end    
          
{{< /mermaid >}}

## Unit Test Cases
| Product Version | UnitTest Id | Description |
|-----------------|-------------|-------------|
| -               | -           | -           |
| -               | -           | -           |

## Security compliance check
1. Only Survey User should Create, View, Update, Delete, Search and Sync the Advertisement Property.

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the USER ROles in the User Manual. It's scope is limited to Developer Technical Documentation

## Feature/Defect list
| Feature/Defect ID | Link                                                     | Status |
|-------------------|----------------------------------------------------------|--------|
| GS-0003           | [GS-0003](https://shadkona.atlassian.net/browse/GS-0003) | Closed |


## References

## Development Estimations
| Release Tag | Feature/Defect ID | Scrum Deatils   | Start date  | End date    |
|-------------|-------------------|-----------------|-------------|-------------|
| 2020OCT     | GS-0002           | Scrum 2020OCTs2 | 14 OCT 2020 | 28 OCT 2020 |

## Feature Doneness Criteria
Check list for the Doneness criteria

| Metric                       | Unit Measure | Expected Result | Actual Result | Accepted? | Remarks               | Approver  |
|------------------------------|--------------|-----------------|---------------|-----------|-----------------------|-----------|
| Acceptance Criteria Defined? | YES or NO    | YES             | YES           | Accepted  | All test cases passed | PM        |
| Architecture Approved?       | YES or NO    | YES             | YES           | Accepted  | Design is accepted    | Architect |
| Coding Completed?            | YES or NO    | YES             | YES           | Completed | Completed             | EM        |
| Product Defects              | Number       | 0               | 0             | Accepted  || EM                    |
| Unit Test Case Count?        | Number       | >5              | 8             | Accepted  | Tested                | EM        |
| Integration Test Cases Count | Number       | >5              | 9             | Accepted  | Tested                | EM        |
| Sonar Vulnerabilities Count  | Number       | 0               | 0             | Accepted  | validated             | EM        |
| Code Coverage                | Number       | >98%            | 99%           | Accepted  | Validated             | EM        |
| User Manual Verified?        | YES or NO    | YES             | YES           | Accepted  | Validated             | DocM      |
| PenTest Defect Count?        | Number       | <2              | 0             | Accepted  | Validated             | EM        |
| PM Accepted?                 | YES or NO    | YES             | YES           | Accepted  | Good to go            | PM        |
| OM Accepted?                 | YES or NO    | YES             | YES           | Accepted  | Good to go            | OM        |
| Deployed to Staging?         | YES or NO    | YES             | YES           | Accepted  | Good to go            | EM        |
| Deployed to Production?      | YES or NO    | YES             | YES           | Accepted  | Good to go            | OM        |




 
