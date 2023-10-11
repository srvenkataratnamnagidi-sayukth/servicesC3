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
1. In Each Locked property (if PropertyName is House) then we have  Property Type,House/Apartment,Apartment Name , Community Name,Door Number,  Street, Location Latitude, Location Longitude, Building Category,Building Sub Category,Land Measurement Type,Length,Breadth,Site Area,Land Survey Number, Land Record Type,Legal Issue,Building Number,Roof Type, Building Floor Type, Construction Status,Construction Completed Date, Plinth Length,Plinth Breadth,Plinth Area fields. 
   1. If House/Apartment  is Apartment then we show the Apartment Name , Community Name otherwise not.Here Apartment Name  is mandatory and Community Optional
   2. If House/Apartment  is Apartment then site area must be in the range of 1-5000 square yards.
   3. If House/Apartment  is Apartment then Only one building is allowed to crate.
   4. If House Category is Concession then we show the House Sub Category field and set the Concession Category Enum Values.
   5. If House Category is Commercial then we show the House Sub Category field and set the Commercial Enum Values.
   6. If House Category is Exemption then we show the House Sub Category field and set the Exemption Enum Values.
   7. If House Category is None or Residential  then we hide the House Sub Category field.
2. If Property Type is Auction then form page has Property Type, Name, Auction Category, Street Name, Location Latitude, Location Longitude fields.
3. If Property Type is Advertisement then form page has Property Type , Name, Street Name , Location Latitude, Location Longitude fields.
4. If Property Type is Trade License then form page has Property Type , Name, Street Name , Location Latitude, Location Longitude fields.
5. If Property Type is Kolagaram then form page has Property Type , Name, Street Name , Location Latitude, Location Longitude fields.
6. If Property Type is Vacant Land then form page has Property Type , Street Name ,Land Category , Land Sub Category, Location Latitude, Location Longitude fields.
   1. If Land Category is Concession then we show the Land Sub Category field and set the Concession Category Enum Values.
   2. If Land Category is Exemption then we show the Land Sub Category field and set the Exemption Enum Values.
   3. If Land Category is Private or Panchyat  then we hide the Land Sub Category field.
6.Only one locked property is allowed with the same name or Door Number.

#### Dependant Features
| Feature name            | Reference Link                                                 | Remarks     |
|-------------------------|----------------------------------------------------------------|-------------|
| Start / Continue Survey | [Start / Continue Survey]({{< ref "StartOrContinueSurvey" >}}) | Parent Page |


#### Use cases
| Use case Code             | Description                   |
|---------------------------|-------------------------------|
| uc_locked_property_create | To create the Locked property |
| uc_locked_property_view   | To view the Locked property   |
| uc_locked_property_update | To update the Locked property |
| uc_locked_property_search | To search the Locked property |
| uc_locked_property_delete | To delete the Locked property |


#### Model Attributes
| Attribute name        | Mandatory | Default value | Input Allowed Char set Layout/API                 | KV Database Key            | SQLite Column Definition     | Create | Update | Remove | View | List | Search | Remarks                                                                              |
|-----------------------|-----------|---------------|---------------------------------------------------|----------------------------|------------------------------|--------|--------|--------|------|------|--------|--------------------------------------------------------------------------------------|
| id                    | YES       | NA            | a-zA-Z0-9, maxlen=128                             | NA                         | id String                    | YES    | YES    | YES    | NO   | NO   | NO     ||
| property_type         | YES       | NA            | 0-9, maxlen=12                                    | PROPERTY_TYPE              | propertyType String          | YES    | YES    | YES    | YES  | YES  | NO     ||
| name                  | YES       | OCR           | a-z A-Z, maxlen=64                                | NAME                       | name String                  | YES    | YES    | YES    | YES  | NO   | NO     ||
| door_number           | YES       | NA            | a-zA-Z0-9.@$_#,:;()/\, maxlen=64                  | DOORNUMBER                 | doorNumber String            | YES    | YES    | YES    | YES  | YES  | NO     ||
| auction_type          | YES       | Choose        | Spinner Values                                    | AUCTION_TYPE_KEY           | aucType String               | YES    | YES    | YES    | YES  | NO   | NO     | Newly added field (13th July 2022)                                                   |
| apartment             | YES       | Choose        | Spinner Values                                    | HOUSE_OR_APARTMENT         | apartment Boolean            | YES    | YES    | YES    | YES  | NO   | NO     | Newly added field (13th July 2022)                                                   |
| apartmentName         | YES       | NA            | a-zA-Z0-9/:#, _.-,@,&, Space, minlen=3, maxlen=64 | APARTMENT_NAME             | apartmentName String         | YES    | YES    | YES    | YES  | NO   | NO     | Newly added filed (13th July 2022)                                                   |
| communityName         | NO        | NA            | a-zA-Z0-9/:#, _.-,@,&, Space, minlen=3, maxlen=64 | COMMUNITY_NAME             | communityName String         | YES    | YES    | YES    | YES  | NO   | NO     | Newly added filed (13th July 2022)                                                   |
| street_name           | YES       | NA            | a-z A-Z, maxlen=32                                | STREET                     | streetName String            | YES    | YES    | YES    | YES  | YES  | NO     ||
| latitude              | YES       | NA            | 0-9.+-, maxlen=24                                 | LATITUDE_KEY               | latitude String              | YES    | YES    | YES    | YES  | NO   | NO     ||
| longitude             | YES       | NA            | 0-9.+-, maxlen=24                                 | LONGITUDE_KEY              | longitude String             | YES    | YES    | YES    | YES  | NO   | NO     ||
| image                 | YES       | NA            | a-zA-Z0-9, maxlen=128                             | PENDING_PROPERTY_IMAGE     | image String                 | YES    | YES    | YES    | YES  | NO   | NO     ||
| house_category        | YES       | NA            | Spinner Values                                    | HOUSE_CATEGORY_KEY_PENDING | houseCategory String         | YES    | YES    | YES    | YES  | NO   | NO     ||
| house_sub_category    | YES       | NA            | Spinner Values                                    | HOUSE_SUB_CATEGORY_KEY     | houseSubCategory String      | YES    | YES    | YES    | YES  | YES  | NO     ||
| vacantLandCategory    | YES       | NA            | Spinner Values                                    | VACANT_LAND_CATEGORY       | vacantLandCategory String    | YES    | YES    | YES    | YES  | NO   | NO     | Newly added filed (13th July 2022)                                                   |
| vacantLandSubCategory | YES       | NA            | Spinner Values                                    | VACANT_LAND_SUB_CATEGORY   | vacantLandSubCategory String | YES    | YES    | YES    | YES  | YES  | NO     | Newly added filed (13th July 2022)                                                   |
| site_length           | YES       | Male          | 0-9,., maxlen=10                                  | SITE_LENGTH_KEY            | siteLength String            | YES    | YES    | YES    | YES  | NO   | NO     ||
| site_breadth          | YES       | NA            | 0-9,., maxlen=10                                  | SITE_BREADTH_KEY           | siteBreadth String           | YES    | YES    | YES    | YES  | NO   | NO     ||
| site_area             | YES       | NA            | 0-9, maxlen=3                                     | SITE_AREA_KEY_PENDING      | siteArea String              | YES    | YES    | YES    | YES  | NO   | NO     ||
| land_survey_number    | YES       | NA            | Spinner Values                                    | LAND_SURVEY_NUMBER_PENDING | landSurveyNumber String      | YES    | YES    | YES    | YES  | NO   | NO     ||
| land_record_type      | YES       | NA            | Spinner Values                                    | LAND_RECORD_TYPE_PENDING   | landRecordType String        | YES    | YES    | YES    | YES  | NO   | NO     ||
| land_measurement_type | YES       | Choose        | Spinner Values                                    | LAND_MEASUREMENT_TYPE      | landMeasurementType String   | YES    | YES    | YES    | YES  | NO   | NO     | This field only visible to user and saved to local db , doesn't  send to the server. |
| legal_issue           | YES       | NA            | 0(No) , 1(Yes)                                    | LEGAL_ISSUE                | legalIssue Boolean           | YES    | YES    | YES    | YES  | NO   | NO     ||
| partitions            | YES       | None          | a-zA-Z0-9, maxlen=128                             | NA                         | partitions String            | YES    | YES    | YES    | YES  | YES  | NO     ||
| dataSync              | YES       | NA            | 0(No) , 1(Yes)                                    | NA                         | dataSync Boolean             | NA     | NA     | NA     | NO   | NO   | NO     ||
| imageSync             | YES       | NA            | 0(No) , 1(Yes)                                    | NA                         | imageSync Boolean            | NA     | NA     | NA     | NO   | NO   | NO     ||
| survey_start_time     | YES       | NA            | a-zA-Z0-9, maxlen=128                             | SURVEY_START_TIME          | survey_start_time String     | YES    | NA     | NA     | YES  | NO   | NO     ||
| survey_end_time       | YES       | NA            | a-zA-Z0-9, maxlen=128                             | SURVEY_END_TIME            | survey_end_time String       | YES    | NA     | NA     | YES  | NO   | NO     ||
| response_error_msg    | YES       | NA            | a-zA-Z0-9, maxlen=NA                              | NA                         | responseErrorMsg String      | NO     | NA     | NA     | YES  | NO   | NO     ||
| is_encrypted          | YES       | NA            | 0(No) , 1(Yes)                                    | NA                         | is_encrypted Boolean         | NA     | NA     | NA     | NO   | NO   | NO     ||


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
SERVICEMEN
EXSERVICEMEN
EXSERVICEMENWIDOW
NONE
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
| Permission code | Action |
|-----------------|--------|
| -               | -      |
| -               | -      |


#### Constraints
| Constraint  | Key  |
|-------------|------|
| Primary Key | id   |
| Unique Keys | name |

## Acceptance Criteria
| Description                                                                                   |
|-----------------------------------------------------------------------------------------------|
| Version : 1.0                                                                                 |
| 1. Survey User can able to Create, View, Update, Search, Delete and Sync the Locked Property. |

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
    Edit[EDIT]-->UnlockBtn[UNLOCK]-->BackButton[<- Back]
{{< /mermaid >}}


### State Machine
{{<mermaid align="left">}}
flowchart TD
	SurveyItemsPage[Survey Dashboard] 
	ListPage((Locked Property List Page))
	FromPage[Locked Property Form Page]
	ConfirmationPage[Locked Property Confirmation Page]
    LockedItem[Locked Property Item]
    ViewPage[Locked Property View Page]
	Start((Start))
    AddBtn[Add Item Button]
    NextBtn1[Next Button]
    FinishBtn1[Finish Button]
    EditBtn[Edit Button]
    BackBtn1[Back Button]
    UnlockBtn[UnLock Button]
    LockedProperty[Locked Property Property]	
    LockedDelteItem[Locked Property Item]
    HousePage[Create House Page]
    AuctionPage[Create Auction Page]
    AdvertisementPage[Create Advertisement Page]
    KolagaramPage[Create Kolagaram Page]
    TradeLicensePage[Create TradeLicense Page]
    VacantPage[Create Vacant Land Page]
    DeleteLockedMessage>Locked Property Deleted]
    End((end))
    ErrorPage>Exception Message]
    Start-->SurveyItemsPage
    subgraph Taxable Properties
        SurveyItemsPage--C-->LockedProperty
	end
    subgraph Error
        LockedProperty--F-->ErrorPage
        ErrorPage-->End
	end	
	subgraph List Page
        LockedProperty--S-->ListPage
        ListPage--C-->AddBtn
        ListPage--C-->LockedItem
        ListPage--SAD-->LockedDelteItem
        LockedDelteItem--F-->ListPage
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
        LockedItem--S-->ViewPage
        LockedItem--F-->ListPage
        ViewPage--C-->EditBtn
        EditBtn--F-->ViewPage
        EditBtn--S-->FromPage
        ViewPage--C-->UnlockBtn
        UnlockBtn--S&PropertyName=House-->HousePage
        UnlockBtn--S&PropertyName=TradeLicense-->TradeLicensePage
        UnlockBtn--S&PropertyName=Kolagaram-->KolagaramPage
        UnlockBtn--S&PropertyName=VacantLand-->VacantPage
        UnlockBtn--S&PropertyName=Advertisement-->AdvertisementPage
        UnlockBtn--S&PropertyName=Auction-->AuctionPage
	end
	subgraph delete
	    LockedDelteItem--S-->LockedKolagaramMessage
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
    ListPage[Kolagaram Listing Page]
    end1((end))
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
    subgraph Unlock 
         CheckPropertyName{Get PropertyName from KV-DB}
    end
    subgraph Unlock Property
          HousePage[Redirected to Create House Page]
          AuctionPage[Redirected to Create Auction Page]
          AdvertisementPage[Redirected to Create Advertisement Page]
          TradePage[Redirected to Create TradeLicense Page]
          KolagaramPage[Redirected to Create Kolagaram Page]
          VacantPage[Redirected to Create VacantLand Page]  
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
    setDataInViewPage--Unlock-->CheckPropertyName
    %%Unlock Property
    CheckPropertyName--IfPropertyName==House-->HousePage
    CheckPropertyName--IfPropertyName==Auction-->AuctionPage
    CheckPropertyName--IfPropertyName==Advertisement-->AdvertisementPage
    CheckPropertyName--IfPropertyName==TradeLicense-->TradePage
    CheckPropertyName--IfPropertyName==Kolagaram-->KolagaramPage
    CheckPropertyName--IfPropertyName==VacantLand-->VacantPage
    HousePage-->end1
    AuctionPage-->end1
    AdvertisementPage-->end1
    TradePage-->end1
    KolagaramPage-->end1
    VacantPage-->end1
  
{{< /mermaid >}}

### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant SQLite as SQLite Database
    participant ListPage as LockedProperty Listing Page
    participant FormPage as LockedProperty Form Page
    participant KVDB as KV Database
    participant ViewPage as LockedProperty View Page
    participant PropertyPage as PropertyCreatePage
    autonumber 
       
    rect rgb(244,244,244)
        ListPage->>+SQLite: load All LockedProperties
        SQLite-->>-ListPage: List Of LockedProperty
    end
    
    rect rgb(244,244,244)
        Note right of FormPage: If (Adding new Locked Property) (3) else { (7) } 
        FormPage->>+KVDB: save LockedProperty KV Data in KVDatabase
    end
    
    rect rgb(244,244,244)
        ViewPage->>+KVDB: get LockedProperty KV Data 
        KVDB-->>-ViewPage: KV LockedProperty Data    
    end  
    rect rgb(244,244,244)
        Note Left of ViewPage: if (Edit == true) {update update LockedProperty} else {insert LockedProperty}
        ViewPage->>+SQLite: updateLockedProperty(LockedProperty) (or) insertLockedProperty(LockedProperty) 
    end  
    
    rect rgb(244,244,244)
        Note right of SQLite: Repeat (1) and (2)
    end
    rect rgb(244,244,244)
        Note left of ViewPage: View LockedProperty Data
        ViewPage->>+SQLite: fetchLockedPropertyById(id) 
        SQLite-->>-ViewPage: LockedProperty Object
    end   
    rect rgb(244,244,244)
        Note left of ViewPage: Edit LockedProperty Data
        FormPage->>+SQLite: fetchLockedPropertyById(id) 
        SQLite-->>-FormPage: LockedProperty Object
    end 
    rect rgb(244,244,244)
         Note right of ViewPage: if (Unlock == true) {Unlock the Property using PropertyName} else {stay in View Page}
         ViewPage->>+PropertyPage: go to respective form page of property type
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
1. Only Survey User should Create, View, Update, Delete, Search and Sync the Locked Property.

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




 
