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
|uc_kolagaram_property_update|To update the kolagaram property|
|uc_kolagaram_property_search|To search the kolagaram property|
|uc_kolagaram_property_delete|To delete the kolagaram property|


#### Model Attributes
| Attribute name     | Mandatory | Default value | Input Allowed Char set Layout/API       | KV Database Key              | SQLite Column Definition  | Create | Update | Remove | View | List | Search | Remarks |
|--------------------|-----------|---------------|-----------------------------------------|------------------------------|---------------------------|--------|--------|--------|------|------|--------|---------|
| id                 | YES       | NA            | a-zA-Z0-9, maxlen=128                   | NA                           | id String                 | YES    | YES    | YES    | NO   | NO   | NO     ||
| aid                | YES       | NA            | 0-9, maxlen=12                          | ADHAR_KEY                    | aid String                | YES    | YES    | YES    | YES  | NO   | NO     ||
| aadhaar_input_type | YES       | OCR           | a-z A-Z, maxlen=128                     | AADHAAR_INPUT_TYPE_KEY       | aadhaar_input_type String | YES    | YES    | YES    | YES  | NO   | NO     ||
| name               | YES       | NA            | a-z A-Z, maxlen=64                      | NAME_KEY                     | name String               | YES    | YES    | YES    | YES  | YES  | NO     ||
| surname            | YES       | NA            | a-z A-Z, maxlen=32                      | SURNAME_KEY                  | surname String            | YES    | YES    | YES    | YES  | NO   | NO     ||
| fsname             | YES       | NA            | a-zA-Z /, maxlen=64                     | FATHER_SPOUSE_NAME_KEY       | fsname String             | YES    | YES    | YES    | YES  | NO   | NO     ||
| mobile_number      | YES       | NA            | 0-9, maxlen=10                          | MOBILE_KEY                   | mobile_number String      | YES    | YES    | YES    | YES  | YES  | NO     ||
| gender             | YES       | Male          | Radio Button Values                     | GENDER_KEY                   | gender String             | YES    | YES    | YES    | YES  | NO   | NO     ||
| dob                | YES       | NA            | 0-9/-, maxlen=10                        | DATE_OF_BIRTH_KEY            | dob String                | YES    | YES    | YES    | YES  | NO   | NO     ||
| age                | YES       | NA            | 0-9, maxlen=3                           | AGE_KEY                      | age String                | YES    | YES    | YES    | YES  | NO   | NO     ||
| kolagaram_name     | YES       | NA            | a-zA-Z0-9.@$_#,:;()/\, maxlen=64        | KOLGARAM_NAME_KEY            | kolagaram_name String     | YES    | YES    | YES    | YES  | YES  | NO     ||
| address            | YES       | NA            | a-zA-Z0-9. /-@&amp;_#,:;()/\, maxlen=64 | KOLGARAM_ADDRESS_KEY         | address String            | YES    | YES    | YES    | YES  | YES  | NO     ||
| gp_sanction_id     | YES       | NA            | a-zA-Z0-9./-@#&amp;_,:, maxlen=32       | GP_SANCTION_KEY              | gp_sanction_id String     | YES    | YES    | YES    | YES  | NO   | NO     ||
| goods_type         | YES       | Choose        | Spinner Values                          | GOODS_TYPE_KEY               | goods_type String         | YES    | YES    | YES    | YES  | YES  | NO     ||
| goods_value        | YES       | NA            | 0-9, maxlen=10                          | GOODS_VALUE_KEY              | goods_value String        | YES    | YES    | YES    | YES  | NO   | NO     ||
| horse_power        | YES       | Choose        | Spinner Values                          | HORSE_POWER_KEY              | horse_power String        | YES    | YES    | YES    | YES  | NO   | NO     ||
| latitude           | YES       | 0.0           | 0-9.+-, maxlen=24                       | LATITUDE_KEY                 | latitude String           | YES    | YES    | YES    | YES  | NO   | NO     ||
| longitude          | YES       | 0.0           | 0-9.+-, maxlen=24                       | LONGITUDE_KEY                | longitude String          | YES    | YES    | YES    | YES  | NO   | NO     ||
| image              | YES       | NA            | a-zA-Z0-9, maxlen=128                   | NA                           | image String              | YES    | YES    | YES    | YES  | NO   | NO     ||
| dataSync           | YES       | NA            | 0(No) , 1(Yes)                          | NA                           | dataSync Boolean          | NA     | NA     | NA     | NO   | NO   | NO     ||
| imageSync          | YES       | NA            | 0(No) , 1(Yes)                          | NA                           | imageSync Boolean         | NA     | NA     | NA     | NO   | NO   | NO     ||
| survey_pending     | YES       | Yes           | 0(No) , 1(Yes)                          | SURVEY_PENDING_KEY           | survey_pending Boolean    | NA     | YES    | NA     | YES  | YES  | NO     ||
| survey_start_time  | YES       | NA            | a-zA-Z0-9, maxlen=128                   | SURVEY_START_TIME            | survey_start_time String  | YES    | NA     | NA     | YES  | NO   | NO     ||
| survey_end_time    | YES       | NA            | a-zA-Z0-9, maxlen=128                   | SURVEY_END_TIME              | survey_end_time String    | YES    | NA     | NA     | YES  | NO   | NO     ||
| avgSurveyTime      | YES       | NA            | a-zA-Z0-9, maxlen=128                   | SURVEY_TIME                  | avgSurveyTime String      | YES    | NA     | NA     | YES  | NO   | NO     ||
| unlockId           | YES       | NA            | a-zA-Z0-9, maxlen=128                   | KOLAGARAM_PROPERTY_UNLOCK_ID | unlockId String           | YES    | NA     | NA     | NO   | NO   | NO     ||
| response_error_msg | YES       | NA            | a-zA-Z0-9, maxlen=NA                    | NA                           | responseErrorMsg String   | NO     | NA     | NA     | YES  | NO   | NO     ||
| is_encrypted       | YES       | NA            | 0(No) , 1(Yes)                          | NA                           | is_encrypted Boolean      | NA     | NA     | NA     | NO   | NO   | NO     ||


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
	SurveyItemsPage[Start / Continue Survey Page] 
	ListPage((Kolagaram Property List Page))
	FromPage[Kolagaram Form Page]
	ConfirmationPage[Kolagaram Details Confirmation Page]
    KolagramItem[Kolagaram Item]
    ViewPage[Kolagram View Page]
	Start((Start))
    AddBtn[Add Item Button]
    NextBtn1[Next Button]
    FinishBtn1[Finish Button]
    EditBtn[Edit Button]
    BackBtn1[Back Button]
    KolagaramProperty[Kolagaram Property]	
    KolagaramDelteItem[Kolagaram Item]
    DeleteKolagaramMessage>Kolagaram Property Deleted]
    End((end))
    ErrorPage>Exception Message]
    Start-->SurveyItemsPage
    subgraph Taxable Properties
        SurveyItemsPage--C-->KolagaramProperty
	end
    subgraph Error
        KolagaramProperty--F-->ErrorPage
        ErrorPage-->End
	end	
	subgraph List Page
        KolagaramProperty--S-->ListPage
        ListPage--C-->AddBtn
        ListPage--C-->KolagramItem
        ListPage--SAD-->KolagaramDelteItem
        KolagaramDelteItem--F-->ListPage
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
        KolagramItem--S-->ViewPage
        KolagramItem--F-->ListPage
        ViewPage--C-->EditBtn
        EditBtn--F-->ViewPage
        EditBtn--S-->FromPage
	end
	subgraph delete
	    KolagaramDelteItem--S-->DeleteKolagaramMessage
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
|:-----|:----|
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
    SurveyDashboard[Start / Continue Survey Page]
    ListPage[Kolagaram Listing Page]
    subgraph List Page
        DBCallLoadAllKolagarams[loadAllKolagarams From SQLite DB]
        SetKolagaramsDatainListPage[Set Kolagaram Data in List Page]
    end
    subgraph Add Item
        FormPage[Kolagaram Form Page]
    end 
    subgraph Form Page
        FormPageInitialSetUp[Kolagaram From Page Initial SetUp]
        saveDatainKVDatabase[save Form Data in KvDataBase]
        DataValidationCehck{Data Validation}
        DetailsConfirmationPage[Kolagaram Details Confirmation Page]
        ShowMessageDataValidation>Show Message: Please Enter Valid Data]
    end
    subgraph Details Confirmation Page
        getDataFromKVDatabase[get Kolagram KV Data From KV Database]
        setDataInConfirmationPage[set Kolagaram Data in Confirmation Page]
        PrepareKolagaramObject[ Kolagaram Object Preparation]
        DBCallInsertOrUpdateKolagaramData[Insert / Update Kolagaram Object in SQLite DB]
    end       
    subgraph View Page
        FetchKolagaramByID[fetchKolagaramById From SQLite DB]
        setDataInViewPage[set Kolagaram Data in Veiw Page]
    end    
    Start-->SurveyDashboard
    SurveyDashboard--Click Kolagaram-->ListPage
    %%List page
    ListPage-->DBCallLoadAllKolagarams
    DBCallLoadAllKolagarams-->SetKolagaramsDatainListPage
    %%Add Kolagaram
    ListPage--Add Kolagaram-->FormPage
    FormPage-->FormPageInitialSetUp
    FormPageInitialSetUp--Input Kolagaram Data-->saveDatainKVDatabase
    saveDatainKVDatabase-->DataValidationCehck
    DataValidationCehck--Valid-->DetailsConfirmationPage
    DataValidationCehck--Not Valid-->ShowMessageDataValidation
    %%Details Confirmation Page
    DetailsConfirmationPage-->getDataFromKVDatabase
    getDataFromKVDatabase-->setDataInConfirmationPage
    setDataInConfirmationPage-->PrepareKolagaramObject
    PrepareKolagaramObject-->DBCallInsertOrUpdateKolagaramData
    DBCallInsertOrUpdateKolagaramData-->DBCallLoadAllKolagarams
    %%Edit Kolagaram
    ListPage--View Kolagaram-->FetchKolagaramByID
    FetchKolagaramByID-->setDataInViewPage
    setDataInViewPage--Edit-->FormPage
    ListPage-->End
{{< /mermaid >}}

### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant SQLite as SQLite Database
    participant ListPage as Kolagaram Listing Page
    participant FormPage as Kolagaram Form Page
    participant KVDB as KV Database
    participant ViewPage as Kolagaram View Page
    autonumber 
       
    rect rgb(244,244,244)
        ListPage->>+SQLite: load All Kolagarams
        SQLite-->>-ListPage: List Of Kolagaram
    end
    
    rect rgb(244,244,244)
        Note right of FormPage: If (Adding new Kolagaram Property) (3) else { (7) } 
        FormPage->>+KVDB: save Kolagaram KV Data in KVDatabase
    end
    
    rect rgb(244,244,244)
        ViewPage->>+KVDB: get Kolagaram KV Data 
        KVDB-->>-ViewPage: KV Kolagaram Data    
    end  
    rect rgb(244,244,244)
        Note Left of ViewPage: if (Edit == true) {update update Kolagaram} else {insert Kolagaram}
        ViewPage->>+SQLite: updateKolagaram(kolagaram) (or) insertKolagaram(kolagaram) 
    end  
    rect rgb(244,244,244)
        Note right of SQLite: Repeat (1) and (2)
    end
    rect rgb(244,244,244)
        Note left of ViewPage: View Kolagram Data
        ViewPage->>+SQLite: fetchKolagaramById(id) 
        SQLite-->>-ViewPage: Kolagaram Object
    end   
    rect rgb(244,244,244)
        Note left of ViewPage: Edit Kolagram Data
        FormPage->>+SQLite: fetchKolagaramById(id) 
        SQLite-->>-FormPage: Kolagaram Object
    end    
    rect rgb(244,244,244)
        Note right of FormPage: Repeat (3) to (6)
    end
    rect rgb(244,244,244)
        Note right of SQLite: Repeat (1) and (2)
    end    
    
    
    
    
    
    
    
          
{{< /mermaid >}}

## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
|-|-|-|
|-|-|-|

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





 
