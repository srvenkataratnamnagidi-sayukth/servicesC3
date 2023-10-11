---
title: House Property
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
1. One citizen can have multiple houses in the same panchayat or in different panchayats.

### Problem Statement
House Property feature is required to store all the house property details in the panchayat level.

### Design 
1. In each House property If OwnHouse is Yes then house module will have House/Apartment, Apartment Name , Community Name, Door Number,Street Name, Block/Ward Number,Building Category,Length,Breadth, Site Area,Land Survey Number,Land Record Type and Legal Issue.
2. If Own House is Yes then we doesn't include Exemption in house category field
3. If Own House is No and house category is Exemption then we didn't take the owner details from the user so that purpose we hide owner details and set the owner details as below.
   1. Name, Sur Name , Father or Spouse Name  are set to be the panchayat name.
   2. Aadhaar Number is set to  be PANCHAYAT_GEO_CODE
   3. Mobile Number is set to be "9000000000"
   4. Date Of Birth is set to be "01-04-1947"
   5. Gender value  is set to be MALE
4. If House/Apartment  is Apartment then site area must be in the range of 1-5000 square yards.
5. If House/Apartment  is Apartment then Only one building is allowed to crate.
6. If House Category is Concession then we show the House Sub Category field and set the Concession Category Enum Values.
7. If House Category is Commercial then we show the House Sub Category field and set the Commercial Enum Values.
8. If House Category is Exemption then we show the House Sub Category field and set the Exemption Enum Values.
9. If House Category is None or Residential  then we hide the House Sub Category field.
10. In each House property If OwnHouse is No then house property will have Aadhaar Input Type,Aadhaar Number,Name,Surname,Father/SpouseName,Mobile Number,Gender,Date Of Birth,Age and Marital Status these are Additional information we take from households. 
11. Each House Module has Building Number, Building Floor Number, Roof Type, Construction Type, Plinth Length, Plinth Breadth, Plinth Area, and Tax Start Date.
12. Each House module have amenities like Private Water Taps,Electricity Connections,LPG Connections,Toilet Count,Soak Pits,Trees Count,Drainage Type, Road Type,Latitude and Longitude.
13. We can Create, Update, View, and remove the house property.
14. Only one house property is allowed with the same Door Number.

#### Checks in the House Module

1. If the Building Category is Concession or Commercial then only we will show Building Sub Category field.
2. In the House/Apartment Field if is Apartment then only we will show Apartment Name and Community Name.
3. Based on the Land Measurement Type we will take the Site Area of the House.
4. Based on the Roof Type we will enable and disable the "Add Floor" Button, if Roof Type is RCC then only we will enable the Add Floor Button.

#### Dependant Features
| Feature name          | Reference Link                                   | Remarks     |
|-----------------------|--------------------------------------------------|-------------|
| Start/Continue Survey | [Start/Continue Survey]({{< ref "side menu" >}}) | Parent Page |


#### Use cases
| Use case Code            | Description                           |
|--------------------------|---------------------------------------|
| uc_house_property_search | To search the house property          |
| uc_house_property_create | To create the house property          |
| uc_house_property_update | To update the house property          |
| uc_house_property_delete | To delete the house property          |
| uc_house_property_view   | To view the house property            |
| uc_house_property_list   | To view the  all the house properties |


#### Model Attributes
##### House Property
#### Model Attributes
| Attribute name          | Mandatory | Default value | Input Allowed Char set Layout/API                 | KV Database Key          | SQLite Column Definition      | Create | Update | Remove | View | List | Search | Remarks                                                                              |
|-------------------------|-----------|---------------|---------------------------------------------------|--------------------------|-------------------------------|--------|--------|--------|------|------|--------|--------------------------------------------------------------------------------------|
| id                      | YES       | NA            | a-zA-Z0-9, maxlen=128                             | NA                       | id String                     | YES    | YES    | YES    | NO   | NO   | NO     ||
| aid                     | YES       | NA            | 0-9, maxlen=12                                    | ADHAR_KEY                | aid String                    | YES    | YES    | YES    | YES  | NO   | NO     ||
| aadhaar_input_type      | YES       | OCR           | a-z A-Z, maxlen=128                               | AADHAAR_INPUT_TYPE_KEY   | aadhaar_input_type String     | YES    | YES    | YES    | YES  | NO   | NO     ||
| name                    | YES       | NA            | a-z A-Z, maxlen=64                                | NAME_KEY                 | name String                   | YES    | YES    | YES    | YES  | YES  | NO     ||
| surname                 | YES       | NA            | a-z A-Z, maxlen=32                                | SURNAME_KEY              | surname String                | YES    | YES    | YES    | YES  | NO   | NO     ||
| fsname                  | YES       | NA            | a-zA-Z /, maxlen=64                               | FATHER_SPOUSE_NAME_KEY   | fsname String                 | YES    | YES    | YES    | YES  | NO   | NO     ||
| mobile_number           | YES       | NA            | 0-9, maxlen=10                                    | MOBILE_KEY               | mobile_number String          | YES    | YES    | YES    | YES  | YES  | NO     ||
| gender                  | YES       | Male          | Radio Button Values                               | GENDER_KEY               | gender String                 | YES    | YES    | YES    | YES  | NO   | NO     ||
| dob                     | YES       | NA            | 0-9/-, maxlen=10                                  | DATE_OF_BIRTH_KEY        | dob String                    | YES    | YES    | YES    | YES  | NO   | NO     ||
| age                     | YES       | NA            | 0-9, maxlen=3                                     | AGE_KEY                  | age String                    | YES    | YES    | YES    | YES  | NO   | NO     ||
| apartment               | YES       | Choose        | Spinner Values                                    | HOUSE_OR_APARTMENT       | apartment Boolean             | YES    | YES    | YES    | YES  | NO   | NO     | Newly added field (13th July 2022)                                                   |
| apartmentName           | YES       | NA            | a-zA-Z0-9/:#, _.-,@,&, Space, minlen=3, maxlen=64 | APARTMENT_NAME           | apartmentName String          | YES    | YES    | YES    | YES  | NO   | NO     | Newly added filed (13th July 2022)                                                   |
| communityName           | NO        | NA            | a-zA-Z0-9/:#, _.-,@,&, Space, minlen=3, maxlen=64 | COMMUNITY_NAME           | communityName String          | YES    | YES    | YES    | YES  | NO   | NO     | Newly added filed (13th July 2022)                                                   |
| door_number             | YES       | NA            | a-zA-Z0-9.@$_#,:;()/\, maxlen=64                  | DOOR_NUMBER_KEY          | doorNumber String             | YES    | YES    | YES    | YES  | YES  | NO     ||
| street_name             | YES       | NA            | a-zA-Z0-9. /-@&amp;_#,:;()/\, maxlen=64           | STREET_KEY               | streetName String             | YES    | YES    | YES    | YES  | YES  | NO     ||
| ward_number             | YES       | 1             | Spinner Values                                    | WARD_NUMBER_KEY          | wardNumber String             | YES    | YES    | YES    | YES  | NO   | NO     ||
| house_category          | YES       | Choose        | Spinner Values                                    | HOUSE_SUB_CATEGORY_KEY   | houseCategory String          | YES    | YES    | YES    | YES  | YES  | NO     ||
| house_sub_category      | YES       | Choose        | Spinner Values                                    | HOUSE_CATEGORY_KEY       | houseSubCategory String       | YES    | YES    | YES    | YES  | NO   | NO     ||
| site_area_length        | YES       | 0             | 0-9, maxlen=4                                     | SITE_AREA_LENGTH_KEY     | siteAreaLength String         | YES    | YES    | YES    | YES  | NO   | NO     ||
| site_area_breadth       | YES       | 0             | 0-9, maxlen=4                                     | SITE_AREA_BREADTH_KEY    | siteAreaBreadth String        | YES    | YES    | YES    | YES  | NO   | NO     ||
| site_area               | YES       | 0             | 0-9., maxlen=8                                    | SITE_AREA_KEY            | siteArea String               | YES    | YES    | YES    | YES  | NO   | NO     ||
| land_survey_number      | YES       | 101           | Spinner Values                                    | LAND_SURVEY_NUMBER       | landSurveyNumber String       | YES    | YES    | YES    | YES  | NO   | NO     ||
| land_record_type        | YES       | Choose        | Spinner Values                                    | LAND_RECORD_TYPE         | landRecordType String         | YES    | YES    | YES    | YES  | NO   | NO     ||
| land_measurement_type   | YES       | Choose        | Spinner Values                                    | LAND_MEASUREMENT_TYPE    | landMeasurementType String    | YES    | YES    | YES    | YES  | NO   | NO     | This field only visible to user and saved to local db , doesn't  send to the server. |
| legal_issue             | YES       | No            | Yes(1),No(0)                                      | LEGAL_ISSUE              | legalIssue Boolean            | YES    | YES    | YES    | YES  | NO   | NO     ||
| water_connections       | YES       | 0             | Spinner Values                                    | PRIVATE_TAPS_KEY         | waterConnections String       | YES    | YES    | YES    | YES  | NO   | NO     ||
| electricity_connections | YES       | 0             | Spinner Values                                    | POWER_CONNECTION_KEY     | electricityConnections String | YES    | YES    | YES    | YES  | NO   | NO     ||
| lpg_connection_count    | YES       | 0             | Spinner Values                                    | LPG_CONNECTION_KEY       | lpgConnectionCount String     | YES    | YES    | YES    | YES  | NO   | NO     ||
| toilet_count            | YES       | 0             | Spinner Values                                    | IHHL_KEY                 | toiletCount String            | YES    | YES    | YES    | YES  | NO   | NO     ||
| soak_pits_count         | YES       | 0             | Spinner Values                                    | SOAK_PITS_KEY            | soakPitsCount String          | YES    | YES    | YES    | YES  | NO   | NO     ||
| trees_count             | YES       | 0             | Spinner Values                                    | TREES_KEY                | treesCount String             | YES    | YES    | YES    | YES  | NO   | NO     ||
| drainage_type           | YES       | Choose        | Spinner Values                                    | DRAINAGE_KEY             | drainageType String           | YES    | YES    | YES    | YES  | NO   | NO     ||
| road_type               | YES       | Choose        | Spinner Values                                    | ROAD_KEY                 | roadType String               | YES    | YES    | YES    | YES  | NO   | NO     ||
| latitude                | YES       | NA            | 0-9.+-, maxlen=24                                 | LATITUDE_KEY             | latitude String               | YES    | YES    | YES    | YES  | NO   | NO     ||
| longitude               | YES       | NA            | 0-9.+-, maxlen=24                                 | LONGITUDE_KEY            | longitude String              | YES    | YES    | YES    | YES  | NO   | NO     ||
| image                   | YES       | NA            | a-zA-Z0-9, maxlen=128                             | NA                       | image String                  | YES    | YES    | YES    | YES  | NO   | NO     ||
| dataSync                | YES       | NA            | 0(No), 1(Yes)                                     | NA                       | dataSync Boolean              | NA     | NA     | NA     | NO   | NO   | NO     ||
| imageSync               | YES       | NA            | 0(No), 1(Yes)                                     | NA                       | imageSync Boolean             | NA     | NA     | NA     | NO   | NO   | NO     ||
| survey_pending          | YES       | Yes           | 0(No), 1(Yes)                                     | SURVEY_PENDING_KEY       | survey_pending Boolean        | NA     | YES    | NA     | YES  | YES  | NO     ||
| survey_start_time       | YES       | NA            | a-zA-Z0-9, maxlen=128                             | SURVEY_START_TIME        | survey_start_time String      | YES    | NA     | NA     | YES  | NO   | NO     ||
| survey_end_time         | YES       | NA            | a-zA-Z0-9, maxlen=128                             | SURVEY_END_TIME          | survey_end_time String        | YES    | NA     | NA     | YES  | NO   | NO     ||
| avgSurveyTime           | YES       | NA            | a-zA-Z0-9, maxlen=128                             | SURVEY_TIME              | avgSurveyTime String          | YES    | NA     | NA     | YES  | NO   | NO     ||
| unlockId                | YES       | NA            | a-zA-Z0-9, maxlen=128                             | HOUSE_PROPERTY_UNLOCK_ID | unlockId String               | YES    | NA     | NA     | NO   | NO   | NO     ||
| response_error_msg      | YES       | NA            | a-zA-Z0-9, maxlen=NA                              | NA                       | responseErrorMsg String       | NO     | NA     | NA     | YES  | NO   | NO     ||
| is_encrypted            | YES       | NA            | 0(No) , 1(Yes)                                    | NA                       | is_encrypted Boolean          | NA     | NA     | NA     | NO   | NO   | NO     ||



##### House Module

#### Model Attributes
| Attribute name            | Mandatory | Default value | Input Allowed Char set Layout/API | KV Database Key         | SQLite Column Definition  | Create | Update | Remove | View | List | Search | Remarks                                                        |
|---------------------------|-----------|---------------|-----------------------------------|-------------------------|---------------------------|--------|--------|--------|------|------|--------|----------------------------------------------------------------|
| house_id                  | YES       | NA            | NA                                | NA                      | id String                 | YES    | YES    | YES    | YES  | NO   | NO     ||
| buildingNumber            | YES       | NA            | Spinner Values                    | BUILDING_NUMBER         | building_number String    | YES    | YES    | NO     | YES  | NO   | NO     ||
| RoofType                  | YES       | NA            | Spinner Values                    | NA                      | roofType String           | YES    | YES    | NO     | YES  | NO   | NO     ||
| buildingFloorType         | YES       | NA            | Spinner Values                    | BUILDING_FLOOR_TYPE_KEY | buildingFloorType String  | YES    | YES    | NO     | YES  | NO   | NO     ||
| ConstructionType          | YES       | NA            | Spinner Values                    | CONSTRUCTION_STATUS_KEY | constructionStatus String | YES    | YES    | NO     | YES  | NO   | NO     ||
| ConstructionCompleted     | NO        | NA            | Age,Year                          | NA                      | NA                        | YES    | NO     | NO     | YES  | NO   | NO     | This field only visible to user , doesn't  send to the server. |
| ConstructionCompletedDate | YES       | NA            | Date                              | CONSTRUCTION_DATE_KEY   | constructionAge String    | YES    | YES    | NO     | YES  | NO   | NO     ||
| plinthLength              | YES       | NA            | 0-9.                              | PLINTH_AREA_LENGTH_KEY  | plinthLength String       | YES    | YES    | NO     | YES  | NO   | NO     ||
| plinthBreadth             | YES       | NA            | 0-9.                              | PLINTH_AREA_BREADTH_KEY | plinthBreadth String      | YES    | YES    | NO     | YES  | NO   | NO     ||
| area                      | YES       | NA            | 0-9.                              | TOTAL_PLINTH_AREA       | plinthArea String         | YES    | YES    | NO     | YES  | NO   | NO     ||


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

##### Concession Category

{{<mermaid align="left">}}
classDiagram
class Name{
SERVICE_MEN
EX_SERVICE_MEN
EX_SERVICEMEN_WIDOW
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

##### Land Measurement Type

{{<mermaid align="left">}}
classDiagram
class Name{
CHOOSE
CENTS
GUNTHAS
YARDS
SQUARE_FEET
LBW
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
| Permission code       | Action                          |
|-----------------------|---------------------------------|
| HOUSE_PROPERTY_CREATE | to Create the House Property    |
| HOUSE_PROPERTY_UPDATE | to Update the House Property    |
| HOUSE_PROPERTY_DELETE | to Delete the House Property    |
| HOUSE_PROPERTY_VIEW   | to View the House Property      |
| HOUSE_PROPERTY_SEARCH | to search in the House Property |


#### Constraints
| Constraint  | Key         |
|-------------|-------------|
| Primary Key | ID          |
| Unique Key  | door_number |


## Acceptance Criteria
| Description                                                                                  |
|----------------------------------------------------------------------------------------------|
| Version : 1.0                                                                                |
| 1. Survey User can able to Create, View, Update, Search, Delete and Sync the House Property. |

## User Experience
### Listing Page
{{<mermaid align="left">}}
graph LR
    Add[+ Add Item]-->Search[Search box]-->BackButton[<- Back]   
{{< /mermaid >}}

### Create House Page
{{<mermaid align="left">}}
graph LR
    Add[+ Add House]
{{< /mermaid >}}

### House Partitions Page
{{<mermaid align="left">}}
graph LR
    Save[Save Button]-->BackButton[<-Back]
{{< /mermaid >}}

### Form Page
{{<mermaid align="left">}}
graph LR
    Next[NEXT]-->BackButton[<- Back]-->AddPartitions[Add Building]
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
	ListPage((House Property List Page))
	FromPage[House Form Page]
	ConfirmationPage[House Confirmation Page]
    HouseItem[House Item]
    ViewPage[House View Page]
	Start((Start))
    AddBtn[Add Item Button]
    AddHouseBtn[Add House]
    NextBtn1[Next Button]
    FinishBtn1[Finish Button]
    EditBtn[Edit Button]
    BackBtn1[Back Button]
    BackBtn2[Back Button]
    HouseProperty[House Property]	
    HouseDelteItem[House Item]
    CreateHouse[Create House Page]
    AddPartitionsBtn[Add Partitions]
    PartitionsPage[Partitions Page]
    SaveBtn[Save]
    DeleteHouseMessage>House Property Deleted]
    End((end))
    ErrorPage>Exception Message]
    Start-->SurveyItemsPage
    subgraph Taxable Properties
        SurveyItemsPage--C-->HouseProperty
	end
    subgraph Error
        HouseProperty--F-->ErrorPage
        ErrorPage-->End
	end	
	subgraph List Page
        HouseProperty--S-->ListPage
        ListPage--C-->AddBtn
        ListPage--C-->HouseItem
        ListPage--SAD-->HouseDelteItem
        HouseDelteItem--F-->ListPage
	end
	subgraph Create House Form
	    AddBtn--S-->CreateHouse
	    CreateHouse--C-->AddHouseBtn
	    AddHouseBtn--F-->CreateHouse
   	end
    subgraph Form Page
         AddHouseBtn--S-->FromPage
         AddBtn--F-->ListPage
         FromPage--C-->NextBtn1
         FromPage--C-->AddPartitionsBtn
         AddPartitionsBtn--F-->FromPage  
   	end
    subgraph Partitions Page
         AddPartitionsBtn--S-->PartitionsPage
         PartitionsPage--C-->SaveBtn     
         SaveBtn--F-->PartitionsPage
         SaveBtn--S-->FromPage
         AddPartitionsBtn--C-->BackBtn2
         BackBtn2--S-->FromPages
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
        HouseItem--S-->ViewPage
        HouseItem--F-->ListPage
        ViewPage--C-->EditBtn
        EditBtn--F-->ViewPage
        EditBtn--S-->FromPage
	end
	subgraph delete
	    HouseDelteItem--S-->DeleteHouseMessage
	end
	%%For click Repressentation
	linkStyle 1 stroke:blue,stroke-width:2px;
	linkStyle 5 stroke:blue,stroke-width:2px;
	linkStyle 6 stroke:blue,stroke-width:2px;
	linkStyle 10 stroke:blue,stroke-width:2px;
	linkStyle 14 stroke:blue,stroke-width:2px;
	linkStyle 15 stroke:blue,stroke-width:2px;
	linkStyle 18 stroke:blue,stroke-width:2px;
	linkStyle 21 stroke:blue,stroke-width:2px;
	linkStyle 25 stroke:blue,stroke-width:2px;
	linkStyle 28 stroke:blue,stroke-width:2px;
	linkStyle 33 stroke:blue,stroke-width:2px;
	%%For success Representation
	linkStyle 4 stroke:green,stroke-width:2px;
	linkStyle 9 stroke:green,stroke-width:2px;
	linkStyle 12 stroke:green,stroke-width:2px;
	linkStyle 17 stroke:green,stroke-width:2px;
	linkStyle 20 stroke:green,stroke-width:2px;
	linkStyle 22 stroke:green,stroke-width:2px;
	linkStyle 24 stroke:green,stroke-width:2px;
	linkStyle 27 stroke:green,stroke-width:2px;
	linkStyle 29 stroke:green,stroke-width:2px;
	linkStyle 31 stroke:green,stroke-width:2px;
	linkStyle 35 stroke:green,stroke-width:2px;
	linkStyle 36 stroke:green,stroke-width:2px;
	%%For failure Representation
	linkStyle 2 stroke:red,stroke-width:2px;
	linkStyle 8 stroke:red,stroke-width:2px;
	linkStyle 11 stroke:red,stroke-width:2px;
	linkStyle 13 stroke:red,stroke-width:2px;
	linkStyle 16 stroke:red,stroke-width:2px;
	linkStyle 19 stroke:red,stroke-width:2px;
	linkStyle 23 stroke:red,stroke-width:2px;
	linkStyle 26 stroke:red,stroke-width:2px;
	linkStyle 30 stroke:red,stroke-width:2px;
	linkStyle 32 stroke:red,stroke-width:2px;
	linkStyle 34 stroke:red,stroke-width:2px;
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

### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant SQLite as SQLite Database
    participant ListPage as House Listing Page
    participant FormPage as House Form Page
    participant Partition as Partition Page
    participant KVDB as KV Database
    participant ViewPage as House View Page
    autonumber 
       
    rect rgb(244,244,244)
        ListPage->>+SQLite: load All Houses
        SQLite-->>-ListPage: List Of Houses
    end
    rect rgb(244,244,244)
        Note right of FormPage: If (Adding new House Property) (5) } 
        FormPage->>+Partition : After Entering site length and breadth go to Patitions page
        Partition->>+FormPage: Added all the Partitons in the House 
        FormPage->>+KVDB: save House KV Data in KVDatabase
    end    
    rect rgb(244,244,244)
        ViewPage->>+KVDB: get House KV Data 
        KVDB-->>-ViewPage: KV House Data    
    end  
    rect rgb(244,244,244)
        Note Left of ViewPage: if (Edit == true) {update update House} else {insert House}
        ViewPage->>+SQLite: updateHouse(House) (or) insertKolagaram(House) 
    end  
    rect rgb(244,244,244)
        Note right of SQLite: Repeat (1) and (2)
    end
    rect rgb(244,244,244)
        Note left of ViewPage: View House Data
        ViewPage->>+SQLite: fetchKolagaramById(id) 
        SQLite-->>-ViewPage: House Object
    end   
    rect rgb(244,244,244)
        Note left of ViewPage: Edit House Data
        FormPage->>+SQLite: fetchHouseById(id) 
        SQLite-->>-FormPage: House Object
    end    
    rect rgb(244,244,244)
        Note right of FormPage: Repeat (3) to (9)
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
1. Only Survey User should Create, View, Search ,Delete and Update House Data.


## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the House Property should be provided in the User Manual.

## Feature/Defect list
| Feature/Defect ID | Link                                                     | Status |
|-------------------|----------------------------------------------------------|--------|
| GS-0003           | [GS-0003](https://shadkona.atlassian.net/browse/GS-0003) | Closed |


## References
1. [Spring Security](https://spring.io/projects/spring-security)
1. [Intro to Spring Security Expressions](https://www.baeldung.com/spring-security-expressions)
1. [Spring Security Role Based Access Authorization Example](https://www.journaldev.com/8748/spring-security-role-based-access-authorization-example)

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




 
