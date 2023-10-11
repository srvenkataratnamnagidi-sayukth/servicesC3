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
1. Each VacantLand property has an Aadhaar Input Type, Land Category , Land Sub Category, photo, owner's Aadhaar number, Name, Surname, Father/Spouse Name, Mobile Number, Gender, Date Of Birth, Age, Street Name, Block/Ward Number, Area, Latitude, Longitude, and Survey Pending Status fields.
2. If Land Category is Concession then we show the Land Sub Category field and set the Concession Category Enum Values.
3. If Land Category is Exemption then we show the Land Sub Category field and set the Exemption Enum Values.
4. If Land Category is Private or Panchyat  then we hide the Land Sub Category field.
5. If Land Category is Exemption then we didn't take the owner details from the user so that purpose we hide owner details and set the owner details as below.
   1. Name, Sur Name , Father or Spouse Name  are set to be the panchyat name.
   2. Aadhaar Number is set to  be PANCHAYAT_GEO_CODE
   3. Mobile Number is set to be "9000000000"
   4. Date Of Birth is set to be "01-04-1947"
   5. Gender value  is set to be MALE
6. Survey User can Create, View, Update, remove and search the VacantLand property.

#### Dependant Features
| Feature name            | Reference Link                                                 | Remarks     |
|-------------------------|----------------------------------------------------------------|-------------|
| Start / Continue Survey | [Start / Continue Survey]({{< ref "StartOrContinueSurvey" >}}) | Parent Page |

#### Use cases
| Use case Code                  | Description                       |
|--------------------------------|-----------------------------------|
| uc_vacant_land_property_create | To create the VacantLand property |
| uc_vacant_land_property_view   | To view the VacantLand property   |
| uc_vacant_land_property_update | To update the VacantLand property |
| uc_vacant_land_property_search | To search the VacantLand property |
| uc_vacant_land_property_delete | To delete the VacantLand property |


#### Model Attributes
| Attribute name        | Mandatory | Default value | Input Allowed Char set Layout/API       | KV Database Key                | SQLite Column Definition     | Create                  | Update | Remove | View | List | Search | Remarks                            |
|-----------------------|-----------|---------------|-----------------------------------------|--------------------------------|------------------------------|-------------------------|--------|--------|------|------|--------|------------------------------------|
| id                    | YES       | NA            | a-zA-Z0-9, maxlen=128                   | NA                             | id String                    | YES                     | YES    | YES    | NO   | NO   | NO     ||
| aid                   | YES       | NA            | 0-9, maxlen=12                          | AADHAR_NUMBER_KEY              | aid String                   | YES                     | YES    | YES    | YES  | NO   | NO     ||
| aadhaar_input_type    | YES       | OCR           | a-z A-Z, maxlen=128                     | AADHAR_INPUT_TYPE_KEY          | aadhaar_input_type String    | YES                     | YES    | YES    | YES  | NO   | NO     ||
| name                  | YES       | NA            | a-z A-Z, maxlen=64                      | NAME_KEY                       | name String                  | YES                     | YES    | YES    | YES  | YES  | NO     ||
| surname               | YES       | NA            | a-z A-Z, maxlen=32                      | SURNAME_KEY                    | surname String               | YES                     | YES    | YES    | YES  | NO   | NO     ||
| fsname                | YES       | NA            | a-zA-Z /, maxlen=64                     | FATHER_NAME_KEY                | fsname String                | YES                     | YES    | YES    | YES  | NO   | NO     ||
| mobile_number         | YES       | NA            | 0-9, maxlen=10                          | MOBILE_NUMBER_KEY              | mobile_number String         | YES                     | YES    | YES    | YES  | YES  | NO     ||
| gender                | YES       | Male          | Radio Button Values                     | GENDER_KEY                     | gender String                | YES                     | YES    | YES    | YES  | NO   | NO     ||
| dob                   | YES       | NA            | 0-9/-, maxlen=10                        | DATEOFBIRTH_KEY                | dob String                   | YES                     | YES    | YES    | YES  | NO   | NO     ||
| age                   | YES       | NA            | 0-9, maxlen=3                           | AGE_KEY                        | age String                   | YES                     | YES    | YES    | YES  | NO   | NO     ||
| address               | YES       | NA            | a-zA-Z0-9. /-@&amp;_#,:;()/\, maxlen=64 | ADDRESS_KEY                    | address String               | YES                     | YES    | YES    | YES  | YES  | NO     ||
| ward_number           | YES       | 1             | Spinner Values                          | WARD_NUMBER_KEY                | wardnumber String            | YES                     | YES    | YES    | YES  | NO   | NO     ||\
| area                  | YES       | NA            | 0-9, maxlen=64                          | AREA_KEY                       | area String                  | YES                     | YES    | YES    | YES  | NO   | NO     ||\
| vacantLandCategory    | YES       | Choose        | Spinner Values                          | VACANT_LAND_CATEGORY           | vacantLandCategory String    | YES                     | YES    | YES    | YES  | NO   | NO     | Newly added filed (13th July 2022) |
| vacantLandSubCategory | YES       | Choose        | Spinner Values                          | VACANT_LAND_SUB_CATEGORY       | vacantLandSubCategory String | YES                     | YES    | YES    | YES  | NO   | NO     | Newly added filed (13th July 2022) |
| latitude              | YES       | 0.0           | 0-9.+-, maxlen=24                       | LATITUDE_KEY                   | latitude String              | YES                     | YES    | YES    | YES  | NO   | NO     ||
| longitude             | YES       | 0.0           | 0-9.+-, maxlen=24                       | LONGITUDE_KEY                  | longitude String             | YES                     | YES    | YES    | YES  | NO   | NO     ||
| image                 | YES       | NA            | a-zA-Z0-9, maxlen=128                   | NA                             | image String                 | YES                     | YES    | YES    | YES  | NO   | NO     ||
| dataSync              | YES       | NA            | 0(No), 1(Yes)                           | NA                             | dataSync Boolean             | NA                      | NA     | NA     | NO   | NO   | NO     ||
| imageSync             | YES       | NA            | 0(No), 1(Yes)                           | NA                             | imageSync Boolean            | NA                      | NA     | NA     | NO   | NO   | NO     ||
| survey_pending        | YES       | Yes           | 0(No), 1(Yes)                           | SURVEY_PENDING_KEY             | survey_pending Boolean       | NA                      | YES    | NA     | YES  | YES  | NO     ||
| survey_start_time     | YES       | NA            | a-zA-Z0-9, maxlen=128                   | SURVEY_START_TIME              | survey_start_time String     | YES                     | NA     | NA     | YES  | NO   | NO     ||
| survey_end_time       | YES       | NA            | a-zA-Z0-9, maxlen=128                   | SURVEY_END_TIME                | survey_end_time String       | YES                     | NA     | NA     | YES  | NO   | NO     ||
| avgSurveyTime         | YES       | NA            | a-zA-Z0-9, maxlen=128                   | SURVEY_TIME                    | avgSurveyTime String         | YES                     | NA     | NA     | YES  | NO   | NO     ||
| unlockId              | YES       | NA            | a-zA-Z0-9, maxlen=128                   | VACANT_LAND_PROPERTY_UNLOCK_ID | unlockId String              | YES                     | NA     | NA     | NO   | NO   | NO     ||
| response_error_msg    | YES       | NA            | a-zA-Z0-9, maxlen=64                    | NA                             | NA                           | responseErrorMsg String | NO     | NA     | NA   | YES  | NO     | NO                                 ||
| is_encrypted          | YES       | NA            | 0(No), 1(YES)                           | NA                             | is_encrypted Boolean         | NA                      | NA     | NA     | NO   | NO   | NO     ||


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

##### Vacant Land Category
{{<mermaid align="left">}}
classDiagram
class Name{
PRIVATE
PANCHAYAT
CONCESSION
EXEMPTION
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

##### Concession Category

{{<mermaid align="left">}}
classDiagram
class Name{
SERVICEMEN
EXSERVICEMEN
EXSERVICEMENWIDOW
NONE
}
{{< /mermaid >}}



#### Feature Permission
| Permission code | Action |
|-----------------|--------|
| -               | -      |
| -               | -      |


#### Constraints
| Constraint  | Key |
|-------------|-----|
| Primary Key | id  |


## Acceptance Criteria
| Description                                                                                       |
|---------------------------------------------------------------------------------------------------|
| Version : 1.0                                                                                     |
| 1. Survey User can able to Create, View, Update, Search, Delete and Sync the VacantLand Property. |

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
	ListPage((VacantLand Property List Page))
	FromPage[VacantLand Form Page]
	ConfirmationPage[VacantLand Details Confirmation Page]
    VacantLandItem[VacantLand Item]
    ViewPage[VacantLand View Page]
	Start((Start))
    AddBtn[Add Item Button]
    NextBtn1[Next Button]
    FinishBtn1[Finish Button]
    EditBtn[Edit Button]
    BackBtn1[Back Button]
    VacantLandProperty[VacantLand Property]	
    VacantLandDeleteItem[VacantLand Item]
    DeleteVacantLandMessage>VacantLand Property Deleted]
    End((end))
    ErrorPage>Exception Message]
    Start-->SurveyItemsPage
    subgraph Taxable Properties
        SurveyItemsPage--C-->VacantLandProperty
	end
    subgraph Error
        VacantLandProperty--F-->ErrorPage
        ErrorPage-->End
	end	
	subgraph List Page
        VacantLandProperty--S-->ListPage
        ListPage--C-->AddBtn
        ListPage--C-->VacantLandItem
        ListPage--SAD-->VacantLandDeleteItem
        VacantLandDeleteItem--F-->ListPage
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
        VacantLandItem--S-->ViewPage
        VacantLandItem--F-->ListPage
        ViewPage--C-->EditBtn
        EditBtn--F-->ViewPage
        EditBtn--S-->FromPage
	end
	subgraph delete
	    VacantLandDeleteItem--S-->DeleteVacantLandMessage
	end
	%%For click Representation
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
    SurveyDashboard[Start / Continue Survey Page]
    ListPage[VacantLand Listing Page]
    subgraph List Page
        DBCallLoadAllVacantLands[loadAllVacantLands From SQLite DB]
        SetVacantLandsDatainListPage[Set VacantLand Data in List Page]
    end
    subgraph Add Item
        FormPage[VacantLand Form Page]
    end 
    subgraph Form Page
        FormPageInitialSetUp[VacantLand From Page SetUp]
        saveDatainKVDatabase[save Form Data in KvDataBase]
        DataValidationCehck{Data Validation}
        DetailsConfirmationPage[VacantLand Details Confirmation Page]
        ShowMessageDataValidation>Show Message: Please Enter Valid Data]
    end
    subgraph Details Confirmation Page
        getDataFromKVDatabase[get VacantLand KV Data From KV Database]
        setDataInConfirmationPage[set VacantLand Data in Confirmation Page]
        PrepareVacantLandObject[ VacantLand Object Preparation]
        DBCallInsertOrUpdateVacantLandData[Insert / Update VacantLand Object in SQLite DB]
    end       
    subgraph View Page
        FetchVacantLandByID[fetchVacantLandById From SQLite DB]
        setDataInViewPage[set VacantLand Data in Veiw Page]
    end    
    Start-->SurveyDashboard
    SurveyDashboard--Click VacantLand-->ListPage
    %%List page
    ListPage-->DBCallLoadAllVacantLands
    DBCallLoadAllVacantLands-->SetVacantLandsDatainListPage
    %%Add VacantLand
    ListPage--Add VacantLand-->FormPage
    FormPage-->FormPageInitialSetUp
    FormPageInitialSetUp--Input VacantLand Data-->saveDatainKVDatabase
    saveDatainKVDatabase-->DataValidationCehck
    DataValidationCehck--Valid-->DetailsConfirmationPage
    DataValidationCehck--Not Valid-->ShowMessageDataValidation
    %%Details Confirmation Page
    DetailsConfirmationPage-->getDataFromKVDatabase
    getDataFromKVDatabase-->setDataInConfirmationPage
    setDataInConfirmationPage-->PrepareVacantLandObject
    PrepareVacantLandObject-->DBCallInsertOrUpdateVacantLandData
    DBCallInsertOrUpdateVacantLandData-->DBCallLoadAllVacantLands
    %%Edit VacantLand
    ListPage--View VacantLand-->FetchVacantLandByID
    FetchVacantLandByID-->setDataInViewPage
    setDataInViewPage--Edit-->FormPage
    ListPage-->End
{{< /mermaid >}}

### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant SQLite as SQLite Database
    participant ListPage as VacantLand Listing Page
    participant FormPage as VacantLand Form Page
    participant KVDB as KV Database
    participant ViewPage as VacantLand View Page
    autonumber 
       
    rect rgb(244,244,244)
        ListPage->>+SQLite: load All VacantLands
        SQLite-->>-ListPage: List Of VacantLand
    end
    
    rect rgb(244,244,244)
        Note right of FormPage: If (Adding new VacantLand Property) (3) else { (7) } 
        FormPage->>+KVDB: save VacantLand KV Data in KVDatabase
    end
    
    rect rgb(244,244,244)
        ViewPage->>+KVDB: get VacantLand KV Data 
        KVDB-->>-ViewPage: KV VacantLand Data    
    end  
    rect rgb(244,244,244)
        Note Left of ViewPage: if (Edit == true) {update update VacantLand} else {insert VacantLand}
        ViewPage->>+SQLite: updateVacantLand(VacantLand) (or) insertVacantLand(VacantLand) 
    end  
    rect rgb(244,244,244)
        Note right of SQLite: Repeat (1) and (2)
    end
    rect rgb(244,244,244)
        Note left of ViewPage: View VacantLand Data
        ViewPage->>+SQLite: fetchVacantLandById(id) 
        SQLite-->>-ViewPage: VacantLand Object
    end   
    rect rgb(244,244,244)
        Note left of ViewPage: Edit VacantLand Data
        FormPage->>+SQLite: fetchVacantLandById(id) 
        SQLite-->>-FormPage: VacantLand Object
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
1. Only Survey User should Create, View, Update, Delete, Search and Sync the VacantLand Property.

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




 
